# 自定义右键菜单demo
核心代码:
```js
window.oncontextmenu = function (ev){
        //阻止默认行为,禁用自带的右键菜单
        ev.preventDefault();
        //没有菜单则创建一个
        let contextxmenu = document.querySelector('.contextxmenu')
        if(!contextxmenu){
            contextxmenu = document.createElement('div')
            contextxmenu.className = 'contextxmenu'
            contextxmenu.innerHTML = `<ul>
                            <li>跳转到首页</li>
                            <li>跳转到详情</li>
                            <li>复制</li>
                        </ul>`
            document.body.appendChild(contextxmenu)
        }
        //控制右键菜单的位置
        contextxmenu.style.left = `${ev.clientX}px`
        contextxmenu.style.top = `${ev.clientY}px`
    }
    //点击其他内容(不包含contetmenu及里面的内容,我们让右键菜单消失)
    window.onclick = function(ev){
        let target = ev.target,
            targetTag = target.tagName

        //点击contentmenu不作任何处理
        if(targetTag === 'LI'){//转化为ul
            target = target.parentNode;
            targetTag = target.tagName
        }
        if(targetTag === 'UL'&& target.parentNode.className==='contextxmenu'){
            return
        }
        //否则让菜单消失
        let contextxmenu = document.querySelector('.contextxmenu')
        if(contextxmenu){
            document.body.removeChild(contextxmenu)
        }

    }
```