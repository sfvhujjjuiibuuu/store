<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>Hansa Store</title>

<style>
body{
    font-family: Arial;
    direction: rtl;
    margin:0;
    background:#f5f5f5;
}

header{
    background:#111;
    color:white;
    padding:15px;
    text-align:center;
}

.topbar{
    text-align:center;
    margin:10px;
}

.topbar button{
    background:#0088cc;
    color:white;
    border:none;
    padding:10px 15px;
    border-radius:8px;
    cursor:pointer;
}

.products{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
}

.card{
    background:white;
    width:220px;
    margin:10px;
    padding:15px;
    border-radius:10px;
    box-shadow:0 0 10px #ccc;
    text-align:center;
}

.price{
    color:green;
    font-weight:bold;
}

button{
    background:green;
    color:white;
    border:none;
    padding:8px;
    margin-top:5px;
    cursor:pointer;
    border-radius:5px;
}

.cart{
    background:white;
    margin:20px;
    padding:15px;
    border-radius:10px;
    box-shadow:0 0 10px #ccc;
}

.remove{
    background:red;
}

.checkoutBox{
    display:none;
    position:fixed;
    top:0;
    right:0;
    width:100%;
    height:100%;
    background:rgba(0,0,0,0.6);
    justify-content:center;
    align-items:center;
}

.checkoutContent{
    background:white;
    padding:20px;
    border-radius:10px;
    width:300px;
    text-align:center;
}

input{
    width:90%;
    padding:8px;
    margin:5px;
}
</style>
</head>

<body>

<header>🎧 Hansa Store - متجر السماعات</header>

<div class="topbar">
    <a href="https://t.me/handsa29" target="_blank">
        <button>💬 تواصل معنا</button>
    </a>
</div>

<div class="products">

    <div class="card">
        <h3>سماعة أمريكي</h3>
        <div class="price">2900 جنيه</div>
        <button onclick="addToCart('سماعة أمريكي',2900)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة فيزا ألماني</h3>
        <div class="price">3500 جنيه</div>
        <button onclick="addToCart('سماعة فيزا ألماني',3500)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>حجر</h3>
        <div class="price">80 جنيه</div>
        <button onclick="addToCart('حجر',80)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة باروكه</h3>
        <div class="price">4000 جنيه</div>
        <button onclick="addToCart('سماعة باروكه',4000)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة ميني</h3>
        <div class="price">4000 جنيه</div>
        <button onclick="addToCart('سماعة ميني',4000)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة حزام</h3>
        <div class="price">4000 جنيه</div>
        <button onclick="addToCart('سماعة حزام',4000)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة توكه</h3>
        <div class="price">4000 جنيه</div>
        <button onclick="addToCart('سماعة توكه',4000)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة مغناطيس</h3>
        <div class="price">3900 جنيه</div>
        <button onclick="addToCart('سماعة مغناطيس',3900)">أضف للسلة</button>
    </div>

    <div class="card">
        <h3>سماعة برا</h3>
        <div class="price">4000 جنيه</div>
        <button onclick="addToCart('سماعة برا',4000)">أضف للسلة</button>
    </div>

</div>

<div class="cart">
    <h2>🛒 السلة</h2>
    <ul id="list"></ul>
    <h3 id="total">الإجمالي: 0</h3>

    <button onclick="openCheckout()">إتمام الشراء 💳</button>
</div>

<div class="checkoutBox" id="checkoutBox">
    <div class="checkoutContent">
        <h3>إتمام الطلب</h3>

        <input id="name" placeholder="الاسم">
        <input id="phone" placeholder="رقم الهاتف">

        <button onclick="pay()">تأكيد الطلب</button>
        <button onclick="closeCheckout()" style="background:red;">إلغاء</button>
    </div>
</div>

<script>
let cart = [];
let total = 0;

function addToCart(name, price){
    cart.push({name,price});
    total += price;
    render();
}

function removeItem(i){
    total -= cart[i].price;
    cart.splice(i,1);
    render();
}

function render(){
    let list = document.getElementById("list");
    list.innerHTML = "";

    cart.forEach((item,i)=>{
        list.innerHTML += `
        <li>
        ${item.name} - ${item.price}
        <button class="remove" onclick="removeItem(${i})">حذف</button>
        </li>`;
    });

    document.getElementById("total").innerText = "الإجمالي: " + total;
}

function openCheckout(){
    if(cart.length === 0){
        alert("السلة فاضية!");
        return;
    }
    document.getElementById("checkoutBox").style.display = "flex";
}

function closeCheckout(){
    document.getElementById("checkoutBox").style.display = "none";
}

function pay(){
    let name = document.getElementById("name").value;
    let phone = document.getElementById("phone").value;

    if(name === "" || phone === ""){
        alert("اكتب البيانات");
        return;
    }

    let msg = "طلب جديد:%0A";
    msg += "الاسم: " + name + "%0A";
    msg += "الموبايل: " + phone + "%0A%0A";

    cart.forEach(i=>{
        msg += i.name + " - " + i.price + "%0A";
    });

    msg += "%0Aالإجمالي: " + total;

    window.open("https://t.me/handsa29", "_blank");
}
</script>

</body>
</html>
