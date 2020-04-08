记录一下使用sectionList 的几个小细节
	1:
		renderSectionHeader 里面的header组件默认在吸顶部
		所以需要stickySectionHeadersEnabled这个字段调为false然后不使用吸顶
	2:
		sectionList的数据必须含有data字段,形如
		`{ key:` `"A"``, data: [{ title:` `"阿童木"`  `}, { title:` `"阿玛尼"`  `}, { title:` `"爱多多"`  `}] },`
		使用renderItem 获取的是数据里的data.这里的意思就是
		data.item.title 指的就是上面数据的data里的title
		而使用renderSectionHeader获取的key值jiu si
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMzk0MTQ5MjFdfQ==
-->