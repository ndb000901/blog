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
|find_elements_by_id(id)|通过元素id属性值定位|
|find_elements_by_name(name)|通过元素name属性值定位元素|
|find_elements_by_class_name(name)|通过元素的class名定位元素|
|find_elements_by_tag_name(name)|通过元素的tag name定位元素|
|find_elements_by_xpath(xpath)|通过XPath定位元素|
|find_elements_by_css_selector(css_selector)|通过css元素选择器定位元素|
|find_elements_by_link_text(link_text)|通过元素标签对之间的文本信息定位|
|find_elements_by_partial_link_text(link_text)|通过元素标签对之间的部分文本信息定位元素|
