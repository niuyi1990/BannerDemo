# BannerDemo
### 自定义的轮播图
##### 使用

      private void init() {
            list.add(R.mipmap.banner_one);
            list.add(R.mipmap.banner_two);
            list.add(R.mipmap.banner_one);
            list.add(R.mipmap.banner_two);

            mBanner.setPages(new CustomBanner.ViewCreator<Integer>() {
                @Override
                public View createView(Context context, int position) {
                    //这里返回的是轮播图的项的布局 支持任何的布局
                    //position 轮播图的第几个项
                    ImageView imageView = new ImageView(context);
                    imageView.setScaleType(ImageView.ScaleType.FIT_XY);
                    return imageView;
                }

                @Override
                public void updateUI(Context context, View view, int position, Integer data) {
                    //在这里更新轮播图的UI
                    //position 轮播图的第几个项
                    //view 轮播图当前项的布局 它是createView方法的返回值
                    //data 轮播图当前项对应的数据
                    Glide.with(context).load(data).into((ImageView) view);
                }
            }, list);

            //设置轮播图的滚动速度
            mBanner.setScrollDuration(500);

            //设置轮播图的点击事件
            mBanner.setOnPageClickListener(new CustomBanner.OnPageClickListener<Integer>() {
                @Override
                public void onPageClick(int position, Integer str) {
                    //position 轮播图的第几个项
                    //str 轮播图当前项对应的数据
                    Toast.makeText(MainActivity.this, position + "", Toast.LENGTH_SHORT).show();
                }
            });
        }

        @Override
        protected void onStart() {
            super.onStart();
            mBanner.startTurning(2000);
        }

        @Override
        protected void onPause() {
            super.onPause();
            //停止轮播图的自动滚动
            mBanner.stopTurning();
        }
    
