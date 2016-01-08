---
layout: post
title: Android Dev Tips #2-实现Android 页面切换的Reveal切换效果
date:       2015-07-13
author:     "Ted"
tags:
    - tips
---


**在Android L之后，出现了很多酷炫的切换效果，模拟水滴展开来切换新页面的效果是其中之一**


----------

 - 实现效果

    ![请输入图片描述][1]

 - 核心代码

        public void startFromLocation(int[] tapLocationOnScreen) {
        changeState(STATE_FILL_STARTED);
        startLocationX = tapLocationOnScreen[0];
        startLocationY = tapLocationOnScreen[1];
        revealAnimator = ObjectAnimator.ofInt(this, "currentRadius", 0,
                getWidth() + getHeight()).setDuration(FILL_TIME);
        revealAnimator.setInterpolator(INTERPOLATOR);
        revealAnimator.addListener(new AnimatorListenerAdapter() {
            @Override
            public void onAnimationEnd(Animator animation) {
                changeState(STATE_FINISHED);
            }
        });
        revealAnimator.start();
        }

 - 项目源码
    [项目GitHub地址][2]


  [1]: http://7xkbzx.com1.z0.glb.clouddn.com/rippleJump.gif
  [2]: https://github.com/xiongwei-git/RippleJump



