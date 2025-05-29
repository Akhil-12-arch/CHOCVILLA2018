const correctPhone = "9490021604";
const correctPassword = "ARAkhil@2012";

const editBtn = document.getElementById('editBtn');
const loginPopup = document.getElementById('loginPopup');
const addBtn = document.getElementById('addItem');
const menuItems = document.getElementById('menuItems');
const placeholder = document.getElementById('placeholder');

let isAdmin = false;

editBtn.onclick = () => {
  if (isAdmin) {
    logout();
  } else {
    loginPopup.style.display = 'flex';
  }
};

function closePopup() {
  loginPopup.style.display = 'none';
}

function checkLogin() {
  const phone = document.getElementById('phone').value;
  const password = document.getElementById('password').value;

  if (phone === correctPhone && password === correctPassword) {
    loginPopup.style.display = 'none';
    enableEditing();
  } else {
    document.getElementById("loginMsg").textContent = "Incorrect phone or password";
  }
}

function enableEditing() {
  isAdmin = true;
  addBtn.style.display = 'block';
  editBtn.textContent = "Logout";
  if (placeholder) placeholder.remove();
}

function logout() {
  isAdmin = false;
  addBtn.style.display = 'none';
  editBtn.textContent = "Edit";
}

addBtn.onclick = () => {
  const item = document.createElement("div");
  item.classList.add("menu-item");

  const imgInput = document.createElement("input");
  imgInput.type = "file";
  imgInput.accept = "image/*";

  const priceInput = document.createElement("input");
  priceInput.type = "text";
  priceInput.placeholder = "Price";

  const removeBtn = document.createElement("button");
  removeBtn.textContent = "×";
  removeBtn.className = "removeBtn";
  removeBtn.onclick = () => item.remove();

  imgInput.onchange = function () {
    const file = this.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = function (e) {
        const img = document.createElement("img");
        img.src = e.target.result;
        imgInput.replaceWith(img);
      };
      reader.readAsDataURL(file);
    }
  };

  item.appendChild(imgInput);
  item.appendChild(priceInput);
  item.appendChild(removeBtn);
  menuItems.appendChild(item);
};
