// Sample login form handling
document.getElementById('loginForm').addEventListener('submit', function(event) {
    event.preventDefault();
    const username = document.getElementById('username').value;
    const password = document.getElementById('password').value;
    alert('Logged in as ' + username);
    document.querySelector('.login-menu').style.display = 'none';
    document.querySelector('.main-website').style.display = 'block';
});

// Product management
let products = [];
let productId = 1;

document.getElementById('addProductBtn').addEventListener('click', function() {
    const productName = prompt('Enter product name:');
    const productPrice = prompt('Enter product price:');
    if (productName && productPrice) {
        products.push({ id: productId++, name: productName, price: productPrice });
        renderProductTable();
    }
});

function renderProductTable() {
    const tbody = document.querySelector('#productTable tbody');
    tbody.innerHTML = '';
    products.forEach(product => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td>${product.id}</td>
            <td>${product.name}</td>
            <td>${product.price}</td>
            <td>
                <button onclick="updateProduct(${product.id})">Update</button>
                <button onclick="deleteProduct(${product.id})">Delete</button>
            </td>
        `;
        tbody.appendChild(row);
    });
}

function updateProduct(id) {
    const product = products.find(p => p.id === id);
    if (product) {
        const newName = prompt('Enter new name:', product.name);
        const newPrice = prompt('Enter new price:', product.price);
        if (newName && newPrice) {
            product.name = newName;
            product.price = newPrice;
            renderProductTable();
        }
    }
}

function deleteProduct(id) {
    products = products.filter(p => p.id !== id);
    renderProductTable();
}

// Initial setup
document.querySelector('.main-website').style.display = 'none';
renderProductTable();
