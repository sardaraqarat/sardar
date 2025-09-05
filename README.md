[index.html](https://github.com/user-attachments/files/22162950/index.html)
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sardara Qarat - موقع العقارات</title>
<style>
  body { font-family: Arial, sans-serif; margin:0; padding:0; background:#f5f5f5; }
  header { background:#004080; color:white; padding:20px; text-align:center; }
  nav { display:flex; justify-content:center; gap:20px; margin:10px 0; }
  nav button { padding:10px 20px; cursor:pointer; border:none; background:#0073e6; color:white; border-radius:5px; }
  nav button.active { background:#004080; }
  .container { display:flex; flex-wrap:wrap; justify-content:center; gap:20px; padding:20px; }
  .property { background:white; border-radius:10px; box-shadow:0 0 10px rgba(0,0,0,0.1); width:300px; overflow:hidden; display:flex; flex-direction:column; }
  .property img { width:100%; height:200px; object-fit:cover; }
  .property .details { padding:15px; }
  .property .details h3 { margin:0 0 10px 0; }
  .property .details p { margin:5px 0; }
  .admin-controls { margin-top:10px; display:flex; justify-content:space-between; }
  .admin-controls button { background:#ff4d4d; color:white; border:none; padding:5px 10px; cursor:pointer; border-radius:5px; }
</style>
</head>
<body>

<header>
  <h1>Sardara Qarat - عقارات</h1>
</header>

<nav>
  <button class="filter-btn active" data-type="all">كل العقارات</button>
  <button class="filter-btn" data-type="sale">للبيع</button>
  <button class="filter-btn" data-type="rent">للإيجار</button>
</nav>

<div class="container" id="properties-container">
  <!-- العقارات ستعرض هنا -->
</div>

<script>
// بيانات العقارات (يمكنك تعديل أو إضافة عقارات جديدة هنا)
let properties = [
  {
    id: 1,
    type: "sale",
    title: "شقة فاخرة للبيع",
    price: "120,000$",
    location: "بغداد، شارع 100",
    floor: "الطابق الثالث",
    image: "https://via.placeholder.com/300x200?text=Sale+1",
    visible: true
  },
  {
    id: 2,
    type: "rent",
    title: "شقة للإيجار",
    price: "350$/شهر",
    location: "أربيل، حي 10",
    floor: "الطابق الثاني",
    image: "https://via.placeholder.com/300x200?text=Rent+1",
    visible: true
  },
  {
    id: 3,
    type: "sale",
    title: "فيلا للبيع",
    price: "250,000$",
    location: "النجف، حي النخيل",
    floor: "الطابق الأرضي",
    image: "https://via.placeholder.com/300x200?text=Sale+2",
    visible: true
  }
];

// دالة عرض العقارات
function displayProperties(type = "all") {
  const container = document.getElementById("properties-container");
  container.innerHTML = "";
  properties.forEach(prop => {
    if(prop.visible && (type === "all" || prop.type === type)){
      container.innerHTML += `
      <div class="property">
        <img src="${prop.image}" alt="${prop.title}">
        <div class="details">
          <h3>${prop.title}</h3>
          <p><strong>السعر:</strong> ${prop.price}</p>
          <p><strong>الموقع:</strong> ${prop.location}</p>
          <p><strong>الطابق:</strong> ${prop.floor}</p>
          <div class="admin-controls">
            <button onclick="hideProperty(${prop.id})">إخفاء</button>
          </div>
        </div>
      </div>`;
    }
  });
}

// دالة إخفاء العقار (للإدارة)
function hideProperty(id) {
  properties = properties.map(prop => {
    if(prop.id === id) prop.visible = false;
    return prop;
  });
  displayProperties(document.querySelector(".filter-btn.active").dataset.type);
}

// الفلاتر
document.querySelectorAll(".filter-btn").forEach(btn => {
  btn.addEventListener("click", () => {
    document.querySelectorAll(".filter-btn").forEach(b => b.classList.remove("active"));
    btn.classList.add("active");
    displayProperties(btn.dataset.type);
  });
});

// عرض جميع العقارات عند تحميل الصفحة
displayProperties();

</script>
</body>
</html>
