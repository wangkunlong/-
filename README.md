# -
慢慢学习吧



//基本配置
/*获取元素*/
/*获取全部元素*/
/*获取元素样式*/
/*设置元素样式*/
/*为元素添加样式*/
/*为元素删除样式*/

/*获取元素*/
var getElem = function(selecter){
	return document.querySelector(selecter);
}

/*获取全部元素*/
var getAllElem = function(selecter){
	return document.querySelectorAll(selecter);
}

/*获取元素样式*/
var getCls = function(element){
	return element.getAttribute('class');
}
/*设置元素样式*/
var setCls = function(element, cls){
	return element.setAttribute('class', cls);
}
/*为元素添加样式*/
var addCls =function(element,cls){
	var baseCls = getCls(element);
	if (baseCls.indexof(cls)===-1) {
		setCls(element,baseCls+' '+cls);
	}
}
/*为元素删除样式*/
var delCls =function(element,cls){
	var baseCls = getCls(element);
	if (baseCls.indexof(cls)!=-1){
		setCls(element,baseCls.split(cls).join(' ') );
	}
}


//第一步， 初始化样式init 页面载入完成后，所有动画元素设置为init
//第二步   页面滚动到那个屏幕，哪个屏幕就播放动画和导航条、大纲的出现
//第三步   导航条双向定位和大纲定位
//第四步   导航条滑动门特效



//第一步， 初始化样式init 页面载入完成后，所有动画元素设置为init
var setScreenAnimateElements ={
	'.screen-1':[
	  '.screen-1__heading',
	  '.screen-1__phone',
	  '.screen-1__shadow',
	],
	'.screen-2' : [
	  '.screen-2__heading',
	  '.screen-2__phone',
	  '.screen-2__subheading',
	  '.screen-2__point',  
	  '.screen-2__point_i_1', 
	  '.screen-2__point_i_2', 
	  '.screen-2__point_i_3', 
	],
	'.screen-3' : [
	  '.screen-3__heading',
	  '.screen-3__phone',
	  '.screen-3__subheading',
	  '.screen-3__feature',  
	  '.screen-3__feature__item', 
	  '.screen-3__feature__item__number', 
	  '.screen-3__feature__item__desc', 
	],
	'.screen-4' : [
	  '.screen-4__heading',
	  '.screen-4__subheading',
	  '.screen-4__type_item_i_1',
	  '.screen-4__type_item_i_2',
	  '.screen-4__type_item_i_3',
	  '.screen-4__type_item_i_4',
	],
	'.screen-5':[
	  '.screen-5__heading',
	  '.screen-5__subheading',
	  '.screen-5__bg',
	],

};
var setScreenAnimateInit =function( screenCls ){//把所有有动画的元素全部设置为init
        var screen = document.querySelector(screenCls);//获取当前屏幕的元素
	    var animateElements = setScreenAnimateElements[screenCls];//需要设置动画的元素
for (var i = 0; i < animateElements.length; i++) {//初始化代码
		var element = document.querySelector(animateElements[i]);
		var baseCls =element.getAttribute('class');
		element.setAttribute('class',baseCls +' '+animateElements[i].substr(1)+'__init')
 	}
}
window.onload = function(){
	for (k in setScreenAnimateElements) {
	setScreenAnimateInit(k);
	}
}

//第二步   页面滚动到那个屏幕，哪个屏幕就播放动画done和导航条、大纲的出现
var playScreenAnimateDone = function(screenCls){
	    var screen = document.querySelector(screenCls);//获取当前屏幕的元素
	    var animateElements = setScreenAnimateElements[screenCls];//需要设置动画的元素
	 for (var i = 0; i < animateElements.length; i++) {
		var element = document.querySelector(animateElements[i]);
		var baseCls =element.getAttribute('class');
		element.setAttribute('class',baseCls.replace('__init','__done'));
 	}
} 

window.onscroll=function(){
	//获取屏幕的高度才能根据滑动的距离来播放
	var top =document.body.scrollTop;
    //导航条、大纲的出现
    // var a = getElem('.header');
    // var b = getElem('.outline');
    // if (top>80) {
    // 	setCls(a,'header__status__back');
    // setCls(b,'outline__status__in');
    // }else{
    // 	setCls(a,'header');
    // setCls(b,'outline');
    // }
   //第二步   页面滚动到那个屏幕，哪个屏幕就播放动画done
	if (top>0) {
		playScreenAnimateDone('.screen-1');
	}
	if (top>800*1) {
		playScreenAnimateDone('.screen-2');
	}
	if (top>800*2) {
		playScreenAnimateDone('.screen-3');

	}
	if (top>800*3) {
		playScreenAnimateDone('.screen-4');

	}
	if (top>800*4) {
		playScreenAnimateDone('.screen-5');

	}

}

//第三步   导航条双向定位和大纲定位
var navItems = getAllElem('.header__nav-item');
var outLineItems = getAllElem('.outline__item');

var setNavJump =function(i,lib){
	var item=lib[i];
	item.onclick=function(){
		document.body.scrollTop = i*800;

	}
}
for (var i = 0; i < navItems.length; i++) {
	setNavJump(i,navItems);
}
for (var i = 0; i < outLineItems.length; i++) {
	setNavJump(i,outLineItems);
}


// // 大纲
// var outLineItems = getAllElem('.outline__item');
// var setyOutLineJump =function(i){
// 	var outLineItem = outline__items[i];
// 	outLineItem.onclick=function(){
// 		document.body.scrollTop = i*800;
// 	}
// }

// for (var i = 0; i < outline__items.length; i++) {
// 	setyOutLineJump(i);
// }
