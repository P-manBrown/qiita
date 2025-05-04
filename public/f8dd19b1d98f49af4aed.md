---
title: 【Rails】Rails APIコントローラーの書き方
tags:
  - Rails
  - API
  - 初学者
private: false
updated_at: '2022-01-26T04:56:41+09:00'
id: f8dd19b1d98f49af4aed
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミング初学者が、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

## Rails APIコントローラーの書き方

```posts_controller.
class Api::V1::PostsController < ApplicationController

  def index
    render json: Post.all
  end

  def show
    render json: Post.find(params[:id])
  end

  def create
    post = Post.new(post_params)
    if post.save
      render json: post
    else
      render json: post.erros, status: 422
    end
  end

  def update
    post = Post.find(params[:id])
    if post.update(post_params)
      render json: post
    else
      render json: post.errors, status: 422
    end
  end

  def destroy
    post = Post.find(params[:id])
    post.destroy
    render json: post
  end

  private
    def post_params
      params.require(:post).permit(:name)
    end
end

```
