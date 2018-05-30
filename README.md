# KIN.table

## Description of parameters
* `wrapperelement` : String containing element selector of where to put the table
* `dataurl` : Url for fetching table data
* `hitsperpage` : Number of hits per page
* `stylesize`	: String "small" smaller font i rows
* `density`	: Column padding, medium is default. Possible values are 'narrow','medium','large'
* `loader`	: Default true, will display a loader on table update
* `loadermsg`	: String with a message to display under the loader
* `columns`	: Array of objects containing configuration of the columns
* `actions`	: Array of objects containing row actions

## Description of column object

## Description of action object

## Example 
```javascript
var table = KIN.table.init({
	wrapperelement	 	: ".custom-table",
	dataurl			: "<%= getPublishedContentUrl %>",
	hitsperpage		: 25,
	stylesize		: 'small',
	density			: 'narrow',
	loader			: true,
	loadermsg		: 'Loading',
	columns : [
			{"type": "1", "columnname":"Title", "columnwidth":"2", "datafield":"title",formatter : formatTitleCol},
			{"type": "1", "columnname":"Publish date", "columnwidth":"2", "datafield":"publishDate"},
			{"type": "1", "columnname":"Modified date", "columnwidth":"3", "datafield":"modifiedDate"},
			{"type": "1", "columnname":"Type", "columnwidth":"3", "datafield":"structureName"},
			{"type": "2", "columnname":"", "columnwidth":"2", "htmlTag":"htmlActionMenu"}
	],
	actions : [
		{"title": '<liferay-ui:message key="edit" />', parameter: "editUrl", "icon": "icon-edit", "image": "", "key":"editPerson",callback:editArticle},
		{"title": '<liferay-ui:message key="delete" />', parameter: {articleId:"$[articleId]",groupId:"$[groupId]"}, "icon": "icon-edit", "image": "", "key":"editPerson",callback:deleteArticle},
		{"title": '<liferay-ui:message key="open" />', parameter: {personType:"Supplier",url:"$[viewurl]",title:"$[title]"}, "icon": "icon-edit", "image": "", "key":"editPerson",callback:openurl},
	 ],
})

/*Example of a callback formatter function*/
function formatTitleCol(obj){
	return '<a class="kingfisher" target="_blank" href="'+obj.item.viewurl+'">'+obj.columnvalue+'</a>';
}

/*Example of action callback functions*/
function editArticle(parameter){
	openEditor(parameter)
}

function deleteArticle(parameters){
	KIN.utils.confirm_custom({
		content : {
			title : 'Confirm',
			message : 'This action will move your article to the recycle bin.'
			},
		theme : 'chili-red',
		onOk:<portlet:namespace />onOkTrashArticle,
		onCancel:<portlet:namespace />onCancel,
		parameters:{
			articleId:parameters.articleId,
			groupId:parameters.groupId
		}
	})
}
```
