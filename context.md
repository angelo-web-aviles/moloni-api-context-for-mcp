TITLE: Moloni API Authentication
DESCRIPTION: Authenticate with the Moloni API using OAuth2 flow to obtain an access token. The API requires a client ID and client secret, which you can obtain by creating an API client in your Moloni account settings.
SOURCE: https://www.moloni.pt/dev/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/grant/ \
  -d "grant_type=password" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "username=YOUR_USERNAME" \
  -d "password=YOUR_PASSWORD"
```

LANGUAGE: javascript
CODE:
```
const authData = {
  grant_type: "password",
  client_id: "YOUR_CLIENT_ID",
  client_secret: "YOUR_CLIENT_SECRET",
  username: "YOUR_USERNAME",
  password: "YOUR_PASSWORD"
};

fetch('https://api.moloni.pt/v1/grant/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(authData)
})
.then(response => response.json())
.then(data => {
  // Store the access token for future requests
  const accessToken = data.access_token;
  console.log('Authentication successful:', data);
})
.catch(error => console.error('Authentication Error:', error));
```

----------------------------------------

TITLE: Moloni API Token Refresh
DESCRIPTION: Refresh your Moloni API access token using a refresh token. This endpoint allows you to obtain a new access token without requiring the user to log in again.
SOURCE: https://www.moloni.pt/dev/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/grant/ \
  -d "grant_type=refresh_token" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "refresh_token=YOUR_REFRESH_TOKEN"
```

LANGUAGE: javascript
CODE:
```
const refreshData = {
  grant_type: "refresh_token",
  client_id: "YOUR_CLIENT_ID",
  client_secret: "YOUR_CLIENT_SECRET",
  refresh_token: "YOUR_REFRESH_TOKEN"
};

fetch('https://api.moloni.pt/v1/grant/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(refreshData)
})
.then(response => response.json())
.then(data => {
  // Store the new access token
  const accessToken = data.access_token;
  console.log('Token refresh successful:', data);
})
.catch(error => console.error('Token Refresh Error:', error));
```

----------------------------------------

TITLE: Get User Information (agentMe)
DESCRIPTION: Retrieve information about the currently authenticated user. This endpoint provides details about the user account that is accessing the Moloni platform through the API.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/agentMe/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

LANGUAGE: javascript
CODE:
```
fetch('https://api.moloni.pt/v1/agentMe/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  }
})
.then(response => response.json())
.then(data => console.log('User Information:', data))
.catch(error => console.error('Error Fetching User Info:', error));
```

----------------------------------------

TITLE: Get All Companies
DESCRIPTION: Retrieve a list of all companies associated with the authenticated user. This endpoint provides basic information about each company including ID, name, and VAT number.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/companies/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

LANGUAGE: javascript
CODE:
```
fetch('https://api.moloni.pt/v1/companies/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  }
})
.then(response => response.json())
.then(data => console.log('Companies:', data))
.catch(error => console.error('Error Fetching Companies:', error));
```

----------------------------------------

TITLE: Get Company Details
DESCRIPTION: Retrieve detailed information about a specific company by providing its ID. The response includes comprehensive company data, including contact information, fiscal details, and settings.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/companies/getOne/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID

fetch('https://api.moloni.pt/v1/companies/getOne/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId
  })
})
.then(response => response.json())
.then(data => console.log('Company Details:', data))
.catch(error => console.error('Error Fetching Company Details:', error));
```

----------------------------------------

TITLE: Update Company Information
DESCRIPTION: Update the details of a specific company by providing its ID and the fields to be updated. This endpoint allows modification of company information such as name, address, and contact details.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/companies/update/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "name=UPDATED_NAME" \
  -d "address=UPDATED_ADDRESS"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const updateData = {
  company_id: companyId,
  name: "Updated Company Name",
  address: "New Company Address",
  zip_code: "12345-678",
  city: "New City"
};

fetch('https://api.moloni.pt/v1/companies/update/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(updateData)
})
.then(response => response.json())
.then(data => console.log('Company Update Result:', data))
.catch(error => console.error('Error Updating Company:', error));
```

----------------------------------------

TITLE: Get All Customers
DESCRIPTION: Retrieve a list of customers for a specific company. You can filter the results by various parameters and paginate the results using the offset and qty parameters.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/customers/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "offset=0" \
  -d "qty=50"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID

fetch('https://api.moloni.pt/v1/customers/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    offset: 0,
    qty: 50
  })
})
.then(response => response.json())
.then(data => console.log('Customers:', data))
.catch(error => console.error('Error Fetching Customers:', error));
```

----------------------------------------

TITLE: Get Customer by ID
DESCRIPTION: Retrieve detailed information about a specific customer by providing their unique customer ID and the company ID they belong to.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/customers/getOne/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "customer_id=CUSTOMER_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const customerId = 789012; // Replace with your customer ID

fetch('https://api.moloni.pt/v1/customers/getOne/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    customer_id: customerId
  })
})
.then(response => response.json())
.then(data => console.log('Customer Details:', data))
.catch(error => console.error('Error Fetching Customer Details:', error));
```

----------------------------------------

TITLE: Insert New Customer
DESCRIPTION: Create a new customer in a specific company. The endpoint requires various customer details like name, VAT number, email, and address information.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "vat": "123456789",
  "number": "CLIENT001",
  "name": "Sample Client",
  "language_id": 1,
  "address": "Sample Street, 123",
  "zip_code": "1234-567",
  "city": "Sample City",
  "country_id": 1,
  "email": "client@example.com",
  "phone": "123456789",
  "website": "https://www.example.com",
  "payment_method_id": 1234,
  "maturity_date_id": 1234,
  "salesman_id": 1234,
  "copies": 1
}
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const newCustomer = {
  company_id: companyId,
  vat: "123456789",
  number: "CLIENT001",
  name: "Sample Client",
  language_id: 1,
  address: "Sample Street, 123",
  zip_code: "1234-567",
  city: "Sample City",
  country_id: 1,
  email: "client@example.com",
  phone: "123456789",
  website: "https://www.example.com",
  payment_method_id: 1234,
  maturity_date_id: 1234,
  salesman_id: 1234,
  copies: 1
};

fetch('https://api.moloni.pt/v1/customers/insert/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(newCustomer)
})
.then(response => response.json())
.then(data => console.log('New Customer Created:', data))
.catch(error => console.error('Error Creating Customer:', error));
```

----------------------------------------

TITLE: Update Customer
DESCRIPTION: Update an existing customer's information in a specific company by providing the customer ID and the fields to be updated.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "customer_id": 654321,
  "name": "Updated Client Name",
  "email": "updated_email@example.com",
  "address": "Updated Street, 456",
  "zip_code": "7654-321",
  "city": "Updated City"
}
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const customerId = 654321; // Replace with your customer ID
const updateData = {
  company_id: companyId,
  customer_id: customerId,
  name: "Updated Client Name",
  email: "updated_email@example.com",
  address: "Updated Street, 456",
  zip_code: "7654-321",
  city: "Updated City"
};

fetch('https://api.moloni.pt/v1/customers/update/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(updateData)
})
.then(response => response.json())
.then(data => console.log('Customer Update Result:', data))
.catch(error => console.error('Error Updating Customer:', error));
```

----------------------------------------

TITLE: Delete Customer
DESCRIPTION: Remove a customer from a specific company by providing the company ID and customer ID. This operation cannot be undone.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/customers/delete/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "customer_id=CUSTOMER_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const customerId = 654321; // Replace with your customer ID

fetch('https://api.moloni.pt/v1/customers/delete/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    customer_id: customerId
  })
})
.then(response => response.json())
.then(data => console.log('Customer Delete Result:', data))
.catch(error => console.error('Error Deleting Customer:', error));
```

----------------------------------------

TITLE: Get All Products
DESCRIPTION: Retrieve a list of products for a specific company. You can filter by category ID and paginate the results using offset and qty parameters.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/products/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "category_id=CATEGORY_ID" \
  -d "offset=0" \
  -d "qty=50"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const categoryId = 12345; // Replace with your category ID

fetch('https://api.moloni.pt/v1/products/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    category_id: categoryId,
    offset: 0,
    qty: 50
  })
})
.then(response => response.json())
.then(data => console.log('Products:', data))
.catch(error => console.error('Error Fetching Products:', error));
```

----------------------------------------

TITLE: Get Product by ID
DESCRIPTION: Retrieve detailed information about a specific product by providing its unique product ID and the company ID it belongs to.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/products/getOne/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "product_id=PRODUCT_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const productId = 345678; // Replace with your product ID

fetch('https://api.moloni.pt/v1/products/getOne/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    product_id: productId
  })
})
.then(response => response.json())
.then(data => console.log('Product Details:', data))
.catch(error => console.error('Error Fetching Product Details:', error));
```

----------------------------------------

TITLE: Insert New Product
DESCRIPTION: Create a new product in a specific company. The endpoint requires product details like name, reference, price, category, and tax information.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "category_id": 123456,
  "type": "1",
  "name": "Sample Product",
  "reference": "PROD001",
  "price": "10.99",
  "unit_id": 12345,
  "has_stock": "1",
  "stock": "100",
  "taxes": [
    {
      "tax_id": 12345,
      "order": 0,
      "cumulative": 0
    }
  ]
}
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const newProduct = {
  company_id: companyId,
  category_id: 123456,
  type: "1",
  name: "Sample Product",
  reference: "PROD001",
  price: "10.99",
  unit_id: 12345,
  has_stock: "1",
  stock: "100",
  taxes: [
    {
      tax_id: 12345,
      order: 0,
      cumulative: 0
    }
  ]
};

fetch('https://api.moloni.pt/v1/products/insert/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(newProduct)
})
.then(response => response.json())
.then(data => console.log('New Product Created:', data))
.catch(error => console.error('Error Creating Product:', error));
```

----------------------------------------

TITLE: Update Product
DESCRIPTION: Update an existing product's information in a specific company by providing the product ID and the fields to be updated.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "product_id": 654321,
  "name": "Updated Product Name",
  "price": "12.99",
  "stock": "75"
}
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const productId = 654321; // Replace with your product ID
const updateData = {
  company_id: companyId,
  product_id: productId,
  name: "Updated Product Name",
  price: "12.99",
  stock: "75"
};

fetch('https://api.moloni.pt/v1/products/update/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(updateData)
})
.then(response => response.json())
.then(data => console.log('Product Update Result:', data))
.catch(error => console.error('Error Updating Product:', error));
```

----------------------------------------

TITLE: Delete Product
DESCRIPTION: Remove a product from a specific company by providing the company ID and product ID. This operation cannot be undone.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/products/delete/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "product_id=PRODUCT_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const productId = 654321; // Replace with your product ID

fetch('https://api.moloni.pt/v1/products/delete/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    product_id: productId
  })
})
.then(response => response.json())
.then(data => console.log('Product Delete Result:', data))
.catch(error => console.error('Error Deleting Product:', error));
```

----------------------------------------

TITLE: Get All Invoices
DESCRIPTION: Retrieve a list of invoices for a specific company. You can filter by customer ID, date range, and document set ID, as well as paginate the results.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/invoices/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "customer_id=CUSTOMER_ID" \
  -d "offset=0" \
  -d "qty=50"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const customerId = 789012; // Replace with your customer ID (optional)

fetch('https://api.moloni.pt/v1/invoices/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    customer_id: customerId,
    offset: 0,
    qty: 50
  })
})
.then(response => response.json())
.then(data => console.log('Invoices:', data))
.catch(error => console.error('Error Fetching Invoices:', error));
```

----------------------------------------

TITLE: Get Invoice by ID
DESCRIPTION: Retrieve detailed information about a specific invoice by providing its unique document ID and the company ID it belongs to.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/invoices/getOne/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "document_id=DOCUMENT_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const documentId = 901234; // Replace with your document ID

fetch('https://api.moloni.pt/v1/invoices/getOne/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    document_id: documentId
  })
})
.then(response => response.json())
.then(data => console.log('Invoice Details:', data))
.catch(error => console.error('Error Fetching Invoice Details:', error));
```

----------------------------------------

TITLE: Create New Invoice
DESCRIPTION: Create a new invoice in a specific company. The endpoint requires details about the customer, products, dates, payment information, and more.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "customer_id": 654321,
  "date": "2023-07-01",
  "expiration_date": "2023-08-01",
  "document_set_id": 12345,
  "products": [
    {
      "product_id": 123456,
      "qty": 2,
      "price": 10.99,
      "discount": 0
    },
    {
      "product_id": 654321,
      "qty": 1,
      "price": 24.99,
      "discount": 5
    }
  ],
  "status": 1
}
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const customerId = 654321; // Replace with your customer ID
const newInvoice = {
  company_id: companyId,
  customer_id: customerId,
  date: "2023-07-01",
  expiration_date: "2023-08-01",
  document_set_id: 12345,
  products: [
    {
      product_id: 123456,
      qty: 2,
      price: 10.99,
      discount: 0
    },
    {
      product_id: 654321,
      qty: 1,
      price: 24.99,
      discount: 5
    }
  ],
  status: 1
};

fetch('https://api.moloni.pt/v1/invoices/insert/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(newInvoice)
})
.then(response => response.json())
.then(data => console.log('New Invoice Created:', data))
.catch(error => console.error('Error Creating Invoice:', error));
```

----------------------------------------

TITLE: Delete Invoice
DESCRIPTION: Remove an invoice from a specific company by providing the company ID and document ID. This operation cannot be undone and may be restricted if the invoice is already certified.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/invoices/delete/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "document_id=DOCUMENT_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const documentId = 901234; // Replace with your document ID

fetch('https://api.moloni.pt/v1/invoices/delete/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    document_id: documentId
  })
})
.then(response => response.json())
.then(data => console.log('Invoice Delete Result:', data))
.catch(error => console.error('Error Deleting Invoice:', error));
```

----------------------------------------

TITLE: Send Invoice by Email
DESCRIPTION: Send a specific invoice to a customer by email. This endpoint allows sending the invoice as a PDF attachment with a customizable message.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/invoices/sendEmail/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "document_id=DOCUMENT_ID" \
  -d "email=RECIPIENT_EMAIL" \
  -d "subject=EMAIL_SUBJECT" \
  -d "message=EMAIL_MESSAGE"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const documentId = 901234; // Replace with your document ID
const emailData = {
  company_id: companyId,
  document_id: documentId,
  email: "customer@example.com",
  subject: "Your Invoice #123",
  message: "Please find attached your invoice. Thank you for your business."
};

fetch('https://api.moloni.pt/v1/invoices/sendEmail/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(emailData)
})
.then(response => response.json())
.then(data => console.log('Email Send Result:', data))
.catch(error => console.error('Error Sending Invoice Email:', error));
```

----------------------------------------

TITLE: Get Stock Movements
DESCRIPTION: Retrieve a list of stock movements for products in a specific company. This endpoint allows tracking inventory changes over time with details about the type of movement, quantity, and related documents.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/productStocks/getMovements/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "product_id=PRODUCT_ID" \
  -d "offset=0" \
  -d "qty=50"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const productId = 345678; // Replace with your product ID

fetch('https://api.moloni.pt/v1/productStocks/getMovements/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    product_id: productId,
    offset: 0,
    qty: 50
  })
})
.then(response => response.json())
.then(data => console.log('Stock Movements:', data))
.catch(error => console.error('Error Fetching Stock Movements:', error));
```

----------------------------------------

TITLE: Create Manual Stock Movement
DESCRIPTION: Create a manual stock entry movement for a product in a specific company. This endpoint allows adjusting stock levels directly without the need for a document.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/productStocks/insert/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "product_id=PRODUCT_ID" \
  -d "warehouse_id=WAREHOUSE_ID" \
  -d "stock=STOCK_AMOUNT" \
  -d "notes=NOTES"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const productId = 345678; // Replace with your product ID
const warehouseId = 56789; // Replace with your warehouse ID
const newStockMovement = {
  company_id: companyId,
  product_id: productId,
  warehouse_id: warehouseId,
  stock: 10,
  notes: "Manual stock adjustment"
};

fetch('https://api.moloni.pt/v1/productStocks/insert/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(newStockMovement)
})
.then(response => response.json())
.then(data => console.log('Stock Movement Created:', data))
.catch(error => console.error('Error Creating Stock Movement:', error));
```

----------------------------------------

TITLE: Get Product Stock Totals
DESCRIPTION: Retrieve the current stock levels for products in a specific company. This endpoint provides a summary of available inventory across all warehouses or filtered by specific criteria.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/productStocks/getTotals/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "category_id=CATEGORY_ID" \
  -d "warehouse_id=WAREHOUSE_ID" \
  -d "offset=0" \
  -d "qty=50"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const categoryId = 0; // 0 for all categories or specify a category ID
const warehouseId = 0; // 0 for all warehouses or specify a warehouse ID

fetch('https://api.moloni.pt/v1/productStocks/getTotals/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    category_id: categoryId,
    warehouse_id: warehouseId,
    offset: 0,
    qty: 50
  })
})
.then(response => response.json())
.then(data => console.log('Product Stock Totals:', data))
.catch(error => console.error('Error Fetching Stock Totals:', error));
```

----------------------------------------

TITLE: Get All Product Categories
DESCRIPTION: Retrieve a list of product categories for a specific company. You can filter by parent category ID and paginate the results.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/productCategories/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "parent_id=PARENT_CATEGORY_ID" \
  -d "offset=0" \
  -d "qty=50"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const parentId = 0; // 0 for top-level categories or a parent ID

fetch('https://api.moloni.pt/v1/productCategories/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    parent_id: parentId,
    offset: 0,
    qty: 50
  })
})
.then(response => response.json())
.then(data => console.log('Product Categories:', data))
.catch(error => console.error('Error Fetching Product Categories:', error));
```

----------------------------------------

TITLE: Insert Product Category
DESCRIPTION: Create a new product category in a specific company. The endpoint requires a name for the category and optionally a parent category ID.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "parent_id": 0,
  "name": "New Category"
}
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const newCategory = {
  company_id: companyId,
  parent_id: 0, // 0 for top-level category or a parent ID
  name: "New Category"
};

fetch('https://api.moloni.pt/v1/productCategories/insert/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(newCategory)
})
.then(response => response.json())
.then(data => console.log('New Category Created:', data))
.catch(error => console.error('Error Creating Category:', error));
```

----------------------------------------

TITLE: Get All Suppliers
DESCRIPTION: Retrieve a list of suppliers for a specific company. You can paginate the results using offset and qty parameters.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/suppliers/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "offset=0" \
  -d "qty=50"
```

----------------------------------------

TITLE: Insert New Supplier
DESCRIPTION: Create a new supplier in a specific company. The endpoint requires similar details as the customer insertion endpoint.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "vat": "123456789",
  "number": "SUPP001",
  "name": "Sample Supplier",
  "language_id": 1,
  "address": "Sample Street, 123",
  "zip_code": "1234-567",
  "city": "Sample City",
  "country_id": 1,
  "email": "supplier@example.com",
  "phone": "123456789",
  "payment_method_id": 1234,
  "maturity_date_id": 1234
}
```

----------------------------------------

TITLE: Get Available Payment Methods
DESCRIPTION: Retrieve a list of available payment methods for a specific company. This information is useful when creating documents that require payment method selection.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/paymentMethods/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID"
```

----------------------------------------

TITLE: Get Available Document Sets
DESCRIPTION: Retrieve a list of document series (sets) for a specific company and document type. This information is required when creating invoices and other documents.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/documentSets/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "document_type_id=DOCUMENT_TYPE_ID"
```

----------------------------------------

TITLE: Get All Warehouses
DESCRIPTION: Retrieve a list of warehouses for a specific company. This information is useful when managing product stock across multiple locations.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/warehouses/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID"
```

----------------------------------------

TITLE: Get Product Stock
DESCRIPTION: Retrieve the stock information for a specific product across all warehouses or for a specific warehouse.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/productStocks/getStockMovement/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "product_id=PRODUCT_ID" \
  -d "warehouse_id=WAREHOUSE_ID"
```

----------------------------------------

TITLE: Update Product Stock
DESCRIPTION: Adjust the stock level for a specific product in a specific warehouse. This endpoint allows you to increase or decrease stock and provide a reason for the adjustment.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "product_id": 654321,
  "warehouse_id": 12345,
  "stock": 10,
  "notes": "Stock adjustment - inventory count"
}
```

----------------------------------------

TITLE: Get All Tax Rates
DESCRIPTION: Retrieve a list of available tax rates for a specific company. This information is required when creating products that need tax information.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/taxes/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID"
```

----------------------------------------

TITLE: Get All Measurement Units
DESCRIPTION: Retrieve a list of measurement units that can be assigned to products in a specific company.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/measurementUnits/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID"
```

----------------------------------------

TITLE: Create Simplified Invoice
DESCRIPTION: Create a simplified invoice for a specific company. This document type is often used for smaller transactions and has fewer required fields than a full invoice.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "customer_id": 654321,
  "date": "2023-07-01",
  "document_set_id": 12345,
  "products": [
    {
      "product_id": 123456,
      "qty": 1,
      "price": 10.99,
      "discount": 0
    }
  ],
  "status": 1
}
```

----------------------------------------

TITLE: Create Credit Note
DESCRIPTION: Create a credit note for a specific company. Credit notes are used to refund or correct invoices that have already been issued.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "customer_id": 654321,
  "date": "2023-07-01",
  "document_set_id": 12345,
  "associated_documents": [
    {
      "document_id": 987654,
      "id": 1
    }
  ],
  "products": [
    {
      "product_id": 123456,
      "qty": 1,
      "price": 10.99,
      "discount": 0
    }
  ],
  "status": 1
}
```

----------------------------------------

TITLE: Create Purchase Order
DESCRIPTION: Create a purchase order for a specific company. Purchase orders are documents sent to suppliers to request products or services.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "supplier_id": 654321,
  "date": "2023-07-01",
  "expiration_date": "2023-08-01",
  "document_set_id": 12345,
  "products": [
    {
      "product_id": 123456,
      "qty": 10,
      "price": 8.99,
      "discount": 0
    }
  ],
  "notes": "Please deliver as soon as possible",
  "status": 1
}
```

----------------------------------------

TITLE: Create Delivery Note
DESCRIPTION: Create a delivery note for a specific company. Delivery notes are documents that accompany goods being delivered to customers.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: json
CODE:
```
{
  "company_id": 123456,
  "customer_id": 654321,
  "date": "2023-07-01",
  "document_set_id": 12345,
  "products": [
    {
      "product_id": 123456,
      "qty": 2,
      "price": 10.99,
      "discount": 0
    }
  ],
  "delivery_method_id": 12345,
  "delivery_datetime": "2023-07-02 14:00:00",
  "status": 1
}
```

----------------------------------------

TITLE: Get Document PDF
DESCRIPTION: Generate and retrieve a PDF version of a specific document. This endpoint returns a base64-encoded string of the PDF file.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/documents/getPDF/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "document_id=DOCUMENT_ID"
```

----------------------------------------

TITLE: Get All Countries
DESCRIPTION: Retrieve a list of countries available in the Moloni platform. This information is useful when creating or updating entities like customers, suppliers, or company details.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/countries/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

LANGUAGE: javascript
CODE:
```
fetch('https://api.moloni.pt/v1/countries/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  }
})
.then(response => response.json())
.then(data => console.log('Countries:', data))
.catch(error => console.error('Error Fetching Countries:', error));
```

----------------------------------------

TITLE: Get All Currencies
DESCRIPTION: Retrieve a list of currencies available in the Moloni platform. This information is useful when configuring company settings or creating documents with specific currency requirements.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/currencies/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

LANGUAGE: javascript
CODE:
```
fetch('https://api.moloni.pt/v1/currencies/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  }
})
.then(response => response.json())
.then(data => console.log('Currencies:', data))
.catch(error => console.error('Error Fetching Currencies:', error));
```

----------------------------------------

TITLE: Get All Languages
DESCRIPTION: Retrieve a list of languages available in the Moloni platform. This information is useful when configuring document templates and communication preferences.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/languages/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

LANGUAGE: javascript
CODE:
```
fetch('https://api.moloni.pt/v1/languages/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  }
})
.then(response => response.json())
.then(data => console.log('Languages:', data))
.catch(error => console.error('Error Fetching Languages:', error));
```

----------------------------------------

TITLE: Get Sales Analysis by Date
DESCRIPTION: Retrieve sales analysis data grouped by date for a specific company. This endpoint provides summarized sales information for reporting and business analysis.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/documents/getSalesByDate/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "start_date=START_DATE" \
  -d "end_date=END_DATE"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const startDate = "2023-01-01";
const endDate = "2023-12-31";

fetch('https://api.moloni.pt/v1/documents/getSalesByDate/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    start_date: startDate,
    end_date: endDate
  })
})
.then(response => response.json())
.then(data => console.log('Sales Analysis by Date:', data))
.catch(error => console.error('Error Fetching Sales Analysis:', error));
```

----------------------------------------

TITLE: Get Sales Analysis by Product
DESCRIPTION: Retrieve sales analysis data grouped by product for a specific company. This endpoint provides insights into product performance and sales trends.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/documents/getSalesByProduct/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "start_date=START_DATE" \
  -d "end_date=END_DATE"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const startDate = "2023-01-01";
const endDate = "2023-12-31";

fetch('https://api.moloni.pt/v1/documents/getSalesByProduct/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    start_date: startDate,
    end_date: endDate
  })
})
.then(response => response.json())
.then(data => console.log('Sales Analysis by Product:', data))
.catch(error => console.error('Error Fetching Product Sales Analysis:', error));
```

----------------------------------------

TITLE: Get All Maturity Dates
DESCRIPTION: Retrieve a list of maturity date options configured in a specific company. These options define payment deadlines that can be applied to documents.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/maturityDates/getAll/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID

fetch('https://api.moloni.pt/v1/maturityDates/getAll/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId
  })
})
.then(response => response.json())
.then(data => console.log('Maturity Dates:', data))
.catch(error => console.error('Error Fetching Maturity Dates:', error));
```

----------------------------------------

TITLE: Create Maturity Date
DESCRIPTION: Create a new maturity date option in a specific company. This endpoint allows defining custom payment deadline options for invoices and other documents.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/maturityDates/insert/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "name=NAME" \
  -d "value=VALUE"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const newMaturityDate = {
  company_id: companyId,
  name: "Net 60",
  value: 60
};

fetch('https://api.moloni.pt/v1/maturityDates/insert/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify(newMaturityDate)
})
.then(response => response.json())
.then(data => console.log('New Maturity Date Created:', data))
.catch(error => console.error('Error Creating Maturity Date:', error));
```

----------------------------------------

TITLE: Check if Database Needs Update
DESCRIPTION: Check if the database needs to be updated or if maintenance is required. This endpoint helps determine if the API is available for normal operations.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/isAllowed/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

LANGUAGE: javascript
CODE:
```
fetch('https://api.moloni.pt/v1/isAllowed/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  }
})
.then(response => response.json())
.then(data => console.log('API Status:', data))
.catch(error => console.error('Error Checking API Status:', error));
```

----------------------------------------

TITLE: Get Document PDF
DESCRIPTION: Generate and retrieve a PDF version of a specific document. This endpoint returns a base64-encoded string of the PDF file.
SOURCE: https://www.moloni.pt/dev/endpoints/

LANGUAGE: bash
CODE:
```
curl -X POST https://api.moloni.pt/v1/documents/getPDF/ \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d "company_id=COMPANY_ID" \
  -d "document_id=DOCUMENT_ID"
```

LANGUAGE: javascript
CODE:
```
const companyId = 123456; // Replace with your company ID
const documentId = 901234; // Replace with your document ID

fetch('https://api.moloni.pt/v1/documents/getPDF/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    company_id: companyId,
    document_id: documentId
  })
})
.then(response => response.json())
.then(data => {
  // PDF data is returned as base64 string
  console.log('PDF Token:', data);
  // You can convert it to a downloadable PDF or embed it
})
.catch(error => console.error('Error Getting PDF:', error));
``` 