---
layout: post
title: Android Dev Tips 1-布局文件XML中的三个小技巧
date:       2015-07-10
author:     "Ted"
tags:
    - Tips
---


* ### 快速绑定点击事件
    - 在XMl中可以通过onClick这个属性直接绑定该视图的点击事件，方法如下：
    
            <Button
                android:id="@+id/pay"
	            android:layout_width="match_parent"
	            android:layout_height="wrap_content"
	            android:layout_margin="10dp"
	            android:onClick="pay"/>
	            
    - 接下来只需在Fragment或者Activity中定义一个public的方法，方法名称需要与xml中定义的一致即可。如下:
    
	        public void pay(View v) {
		        //todo something
            }

* ### 避免XML中硬编码检查
    - XML文件对String的引用，通常的建议是写在string.xml文件中，否则会出现硬编码相关的警告，如下图:
    
		![图片1][1]  
	
    - 避免这个警告很简单，使用命名空间Tools中的一个属性即可解决：
    
			<Button
				android:id="@+id/pay"
				android:layout_width="match_parent"
		        android:layout_height="wrap_content"
		        android:layout_margin="10dp"
		        android:onClick="pay"
		        android:text="支付"
		        tools:ignore="HardcodedText" />  

	同样解决方案可参考：http://stackoverflow.com/questions/14940255/how-to-remove-error-hardcoded-string-button-should-use-string-resource-in-ecli

* ### 实时预览中的文本内容不带到生产环境中
    - XMl中为了实时预览，我们通常都会写上一些假数据，如上面这段代码中的“支付”，但是我其实并不像把这段文字带到生产环境中去，如何实现呢，上线前，一个个删除？太麻烦啦。Tools的另外一个功能来帮助你，如下代码即可
			
			<Button
	            android:id="@+id/pay"
	            android:layout_width="match_parent"
	            android:layout_height="wrap_content"
	            android:layout_margin="10dp"
	            android:onClick="pay"
	            tools:text = "支付"
	            tools:ignore="HardcodedText" />

  [1]: http://7xkbzx.com1.z0.glb.clouddn.com/0712_1.png
