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
|size|返回元素大小|
|tag_name|标签名|
|text|元素文本|

**一些方法**

|方法|说明|
|----|----|
|clear()|清除文本框或文本域内容|
|click()|点击|
|send_keys(value)|模拟输入文本|
|submit()|提交该元素所属表单内容|
|is_displayed()|是否可见|
|get_attribute(name)|获取属性值|
|is_enabled()|是否可用|
|is_selected()|是否被选中，用于复选框、单选按钮|
|value_of_css_property(property_name)|获取css属性的值|

## 5.Select

**Select类用于处理下拉菜单和列表**

**一些属性**

|属性|说明|
|----|----|
|all_selected_options|获取下拉菜单与列表中被选中的所有内容|
|first_selected_option|获取下拉菜单和列表的第一个选项或当前选择项|
|options|获取下拉菜单和列表的所有选项|

**一些方法**

|方法|说明|
|----|----|
|deselect_all()|清除所有选择项|
|deselect_by_index(index)|根据索引清除选择项|
|deselect_by_value(value)|清除所有与给定值匹配的选项|
|deselect_by_visible_text(text)|清除所有与给定text匹配的选择项|
|select_by_index(index)|根据索引选择|
|select_by_value(value)|选择所有与给定值匹配的选项|
|select_by_visible_text(text)|选择所有与给定text匹配的选择项|


## 6.Alert

**一些属性**

|属性|说明|
|----|----|
|text|获取警告窗口文本|

**一些方法**

|方法|说明|
|----|----|
|accept()|接受警告，单击OK|
|dismiss()|驳回警告，单击取消|
|send_keys(value)|模拟输入|


## 7.等待机制

**隐式等待**

WebDriver将会在指定的时间内查找元素，超时后抛出NoSuchElementException异常。

```
implicitly_wait(time)
```

**显示等待**

WebDriver 提供 WebDriverWait、expected_conditions实现显示等待。

[expected_conditions 文档](https://www.selenium.dev/selenium/docs/api/py/webdriver_support/selenium.webdriver.support.expected_conditions.html#module-selenium.webdriver.support.expected_conditions)


## 8.键盘、鼠标事件

**ActionChains类实现**

**一些方法**

|方法|说明|
|----|----|
|click(on_element=None)|单击元素，若参数为None则点击当前鼠标位置|
|double_click(on_element=None)|双击元素，若参数为None则点击当前鼠标位置|
|click_and_hold(on_element)|按住鼠标左键，若参数为None则点击当前鼠标位置|
|drag_and_drop(source,target)|拖动鼠标，source鼠标拖动的源元素，target鼠标释放的目标元素|
|key_down(value,element=None)|按下某修饰键，在Keys定义，element=None,按键在当前焦点|
|key_up(value,element=None)|松开某修饰键，在Keys定义，element=None,按键在当前焦点|
|send_keys(value)|模拟键盘输入|
|move_to_element(element)|将鼠标移至目标元素|
|release(on_element=None)|释放鼠标,on_element为被鼠标释放的元素|
|perform()|提交已保存的动作|
|send_keys_to_element(element,keys_to_send)|对指定元素的键盘操作，element指定的元素，keys_to_send键盘输入值|

## 9.执行JavaScript

**一些方法**

|方法|说明|
|----|----|
|execute_async_script(script,*args)|异步执行|
|execute_script(script,*args)|同步执行|


## 10.屏幕截图

**一些方法**

|方法|说明|
|----|----|
|save_screenshot(filename)|截屏保存|
|save_screenshot_as_base64()|返回当前截屏base64编码字符串|
|get_screenshot_as_file(filename)|获取当前的屏幕截图，使用完整路径|
|get_screenshot_as_png|获取当前屏幕截图的二进制文件数据|

## 11.录屏

安装第三方包

```
pip install Castro
```

## 12.操作cookies

**一些方法**

|方法|说明|
|----|----|
|add_cookie(cookie_dict)|添加cookie,cookie_dict字典|
|delete_all_cookies()|删除当前会话所有cookie|
|delete_cookie(name)|删除单个名叫name的cookie|
|get_cookies()|返回所有cookie信息|
|get_cookie(name)|返回单个名为name的cookie|

