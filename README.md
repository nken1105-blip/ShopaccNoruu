<!DOCTYPE html><html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SHOP LIÊN QUÂN LEVEL TỐI ĐA</title><style>
body{
margin:0;
font-family:Arial;
background:#020617;
color:white;
}

header{
background:#020617;
padding:15px;
display:flex;
justify-content:space-between;
align-items:center;
border-bottom:1px solid #9333ea;
}

.logo{
font-size:24px;
font-weight:bold;
color:#a855f7;
}

nav button{
margin-left:10px;
}

.container{
max-width:1200px;
margin:auto;
padding:20px;
}

.banner{
background:linear-gradient(90deg,#9333ea,#2563eb);
padding:50px;
text-align:center;
border-radius:12px;
margin-bottom:20px;
box-shadow:0 0 30px #9333ea;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:15px;
}

.card{
background:#0f172a;
border-radius:12px;
overflow:hidden;
transition:0.3s;
position:relative;
}

.card:hover{
transform:scale(1.07);
box-shadow:0 0 25px #9333ea;
}

.card img{
width:100%;
height:160px;
object-fit:cover;
}

.card-body{
padding:10px;
}

.id{
color:#64748b;
font-size:12px;
}

.price{
color:#22c55e;
font-size:20px;
font-weight:bold;
}

.vip{
position:absolute;
top:5px;
left:5px;
background:gold;
color:black;
padding:3px 6px;
border-radius:6px;
font-size:12px;
}

button{
padding:8px;
border:none;
border-radius:8px;
background:#9333ea;
color:white;
cursor:pointer;
}

button:hover{
background:#7e22ce;
}

.topbar{
display:flex;
justify-content:space-between;
margin-bottom:15px;
flex-wrap:wrap;
gap:10px;
}

.stats{
display:flex;
gap:10px;
}

.stat{
background:#0f172a;
padding:10px;
border-radius:10px;
}

.modal{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.9);
display:none;
justify-content:center;
align-items:center;
}

.modal-box{
background:#0f172a;
padding:20px;
border-radius:12px;
max-width:400px;
}

.admin{
display:none;
margin-top:20px;
background:#0f172a;
padding:15px;
border-radius:10px;
}

input{
padding:8px;
margin:5px;
border-radius:6px;
border:none;
width:95%;
}

</style></head>
<body><header>
<div class="logo">SHOP LIÊN QUÂN MAX</div>
<nav>
<button onclick="openBlind()">Túi mù</button>
<button onclick="login()">Admin</button>
</nav>
</header><div class="container"><div class="banner">
<h1>SHOP ACC LIÊN QUÂN TỰ ĐỘNG</h1>
<p>Uy tín - Nhanh - Tự động 100%</p>
</div><div class="topbar">
<input id="search" placeholder="Tìm acc..." oninput="render()">
<div class="stats">
<div class="stat">Acc: <span id="total"></span></div>
<div class="stat">Đã bán: <span id="sold">0</span></div>
</div>
</div><div class="grid" id="shop"></div><div class="admin" id="adminPanel">
<h3>Thêm acc</h3>
<input id="name" placeholder="Tên acc">
<input id="skin" placeholder="Skin">
<input id="rank" placeholder="Rank">
<input id="price" placeholder="Giá">
<input id="img" placeholder="Link ảnh">
<button onclick="addAcc()">Thêm</button>
</div></div><div class="modal" id="modal">
<div class="modal-box" id="modalBox"></div>
</div><script>
let password="admin123";
let sold=0;

let accs=JSON.parse(localStorage.getItem("accs"))||[];

function save(){
localStorage.setItem("accs",JSON.stringify(accs));
}

function render(){
let shop=document.getElementById("shop");
let search=document.getElementById("search").value.toLowerCase();

shop.innerHTML="";

accs.filter(acc=>acc.name.toLowerCase().includes(search)).forEach(acc=>{

shop.innerHTML+=`

<div class="card" onclick="view(${acc.id})">
<div class="vip">VIP</div>
<img src="${acc.img}">
<div class="card-body">
<div class="id">ID: ${acc.id}</div>
<h3>${acc.name}</h3>
<p>Skin: ${acc.skin}</p>
<p>Rank: ${acc.rank}</p>
<div class="price">${acc.price.toLocaleString()}đ</div>
<button onclick="buy(event,${acc.id})">Mua ngay</button>
</div>
</div>

`;

});


document.getElementById("total").innerText=accs.length;
}

function view(id){
let acc=accs.find(a=>a.id==id);
modalBox.innerHTML=`
<h2>${acc.name}</h2>
<img src="${acc.img}" width="100%">
<p>ID: ${acc.id}</p>
<p>Skin: ${acc.skin}</p>
<p>Rank: ${acc.rank}</p>
<p>${acc.price.toLocaleString()}đ</p>
<button onclick="buy(event,${acc.id})">Thanh toán</button>
`;
modal.style.display="flex";
}

modal.onclick=()=>modal.style.display="none";

function buy(e,id){
e.stopPropagation();
sold++;
document.getElementById("sold").innerText=sold;
alert("Thanh toán thành công. Admin sẽ gửi acc.");
}

function openBlind(){
if(accs.length==0) return alert("Không có acc");
let acc=accs[Math.floor(Math.random()*accs.length)];
alert("Bạn nhận được acc ID "+acc.id);
}

function login(){
let pass=prompt("Nhập mật khẩu admin");
if(pass==password){
adminPanel.style.display="block";
alert("Đăng nhập thành công");
}else alert("Sai mật khẩu");
}

function addAcc(){
let acc={
id:Math.floor(Math.random()*999999),
name:name.value,
skin:skin.value,
rank:rank.value,
price:Number(price.value),
img:img.value
};

accs.push(acc);
save();
render();
}

render();
</script></body>
</html>
