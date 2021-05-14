# python自动化——Selenium

## 1.实验环境

>1.manjaro21-gnome
>
>2.python3.8
>
>3.chrome-90.0.4430.212
>
>4.selenium-3.141
>
>5.chromedriver
>

**注意：** chromedriver下载与自己浏览器相符的版本，selenium也可用于其他浏览器，下载与浏览器相应的*driver就好。


## 2.定位元素

selenium 提供8种find_element_by定位元素的方法，有16个函数，分为两类find_element_by 返回匹配的第1个元素，find_elements_by返回所有匹配的元素。

**表1**

|方法|说明|
|----|----|
|find_element_by_id(id)|通过元素id属性值定位|
|find_element_by_name(name)|通过元素name属性值定位元素|
|find_element_by_class_name(name)|通过元素的class名定位元素|
|find_element_by_tag_name(name)|通过元素的tag name定位元素|
|find_element_by_xpath(xpath)|通过XPath定位元素|
|find_element_by_css_selector(css_selector)|通过css元素选择器定位元素|
|find_element_by_link_text(link_text)|通过元素标签对之间的文本信息定位|
|find_element_by_partial_link_text(link_text)|通过元素标签对之间的部分文本信息定位元素|

**表2**

|方法|说明|
|----|----|
|find_elements_by_id(id)|通过元素id属性值定位|
|find_elements_by_name(name)|通过元素name属性值定位元素|
|find_elements_by_class_name(name)|通过元素的class名定位元素|
|find_elements_by_tag_name(name)|通过元素的tag name定位元素|
|find_elements_by_xpath(xpath)|通过XPath定位元素|
|find_elements_by_css_selector(css_selector)|通过css元素选择器定位元素|
|find_elements_by_link_text(link_text)|通过元素标签对之间的文本信息定位|
|find_elements_by_partial_link_text(link_text)|通过元素标签对之间的部分文本信息定位元素|

## 3.WebDriver

**一些属性**

|属性|说明|
|----|----|
|current_url|返回当前页面url|
|name|返回浏览器名称|
|title|获取当前页面标题|
|page_source|返回当前页面源码|
|current_window_handle|获取当前窗口的句柄|
|window_handles|获取当前session所有窗口句柄|
|orientation|获取当前设备方位|

**一些方法**

|方法|说明|
|----|----|
|back()|后退|
|forward()|前进|
|close()|关闭当前浏览器窗口|
|get(url)|访问url|
|quit()|退出当前driver并关闭所有相关窗口|
|refresh()|刷新当前页面|
|maximize_window()|最大化窗口|
|switch_to_active_element()|返回当前焦点所在元素|
|switch_to_alert()|切换焦点至弹出的警告|
|switch_to_default_content()|切换焦点至默认框架|
|switch_to_window(window_name)|切换焦点到指定窗口|
|switch_to.frame(frame_reference)|通过索引、名称、元素将焦点切换至指定框架，也适用于iframes|
|implicitly_wait(time_to_wait)|设置目标元素被找到，或指令完成等待超时时间|
|set_page_load_timeout(time_to_wait)|设置一个页面完全加载的超时等待时间|
|set_script_timeout(time_to_wait)|设置脚本执行的超时时间|

## 4.WebElement

**一些属性**

|属性|说明|
|----|----|
|||
|||
|||

**一些方法**

|方法|说明|
|----|----|
|||
|||
|||
|||
|||
|||
|||
|||
|||
