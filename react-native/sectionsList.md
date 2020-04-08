记录一下使用sectionList 的几个小细节
	1:
		renderSectionHeader 里面的header组件默认在吸顶部
		所以需要stickySectionHeadersEnabled这个字段调为false然后不使用吸顶
	2:
		sectionList的数据必须含有data字段,形如
		`{ key:` `"A"``, data: [{ title:` `"阿童木"`  `}, { title:` `"阿玛尼"`  `}, { title:` `"爱多多"`  `}] },`
		
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzQxODgyMTldfQ==
-->