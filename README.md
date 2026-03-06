<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>网址收藏工具</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:system-ui, sans-serif}
body{background:#f2f5f9;padding:20px;max-width:700px;margin:0 auto}
.card{background:#fff;border-radius:12px;padding:20px;box-shadow:0 2px 10px #0001; margin-bottom:20px}
h1{font-size:22px;margin-bottom:16px;color:#222}
input{width:100%;padding:12px 14px;border:1px solid #ddd;border-radius:8px;font-size:16px;outline:none;margin-bottom:10px}
input:focus{border-color:#007bff}
button{padding:12px 20px;background:#007bff;color:white;border:none;border-radius:8px;font-size:16px;cursor:pointer}
button:hover{background:#0066d3}
.item{display:flex;justify-content:space-between;align-items:center;padding:12px 0;border-bottom:1px solid #f0f0f0}
.item a{color:#007bff;text-decoration:none;word-break:break-all;max-width:80%}
.del{color:#ff4444;cursor:pointer}
</style>
</head>
<body>

<div class="card">
  <h1>网址收藏夹</h1>
  <input id="url" placeholder="输入网址，例如 baidu.com">
  <button onclick="add()">添加并打开</button>
</div>

<div class="card">
  <h1>我的收藏</h1>
  <div id="list"></div>
</div>

<script>
const list = document.getElementById('list')
const input = document.getElementById('url')
let links = JSON.parse(localStorage.getItem('links') || '[]')

render()

function add(){
  let v = input.value.trim()
  if(!v)return
  if(!v.startsWith('http')) v = 'https://'+v
  links.unshift(v)
  localStorage.setItem('links', JSON.stringify(links))
  input.value = ''
  render()
  window.open(v, '_blank')
}

function render(){
  list.innerHTML = ''
  links.forEach((u,i)=>{
    const div = document.createElement('div')
    div.className='item'
    div.innerHTML = `
      <a href="${u}" target="_blank">${u}</a>
      <span class="del" onclick="del(${i})">删除</span>
    `
    list.appendChild(div)
  })
}

function del(i){
  links.splice(i,1)
  localStorage.setItem('links', JSON.stringify(links))
  render()
}
</script>
</body>
</html>
