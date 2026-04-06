customer[icon:user]{
  customer_id serial pk  
  name varchar(50)     
  createdAt timestamp  
  updatedAt timestamp
}

address [icon:map-pin] {
  address_id serial pk     
  customer_id fk not null   
  street varchar(24) null
  colony varchar(24) not null
  city varchar(24) not null
  state varchar(24) not null
  pincode number not null
}

product[icon:shopping-bag]{
  product_id serial pk
  type varchar(20) not null
  color varchar(24) null
  size number null
  quantity number not null
  condition enum["new" "good" "decent"] null
  price not null
  createdAt timestamp
  updatedAt timestamp
}

orders [icon:shopping-cart]{
order_id serial pk
customer_id fk not null
shipping_status varchar(12)
total_amount number
createdAt timestamp
updatedAt timestamp
}

order_item{
  orderitem_id serial pk
  order_id fk
  product_id fk
  quantity number
  ordering_date Date
  amount number
  createdAt timestamp
  updatedAt timestamp
}

payment[icon:money]{
payment_id serial pk
order_id fk
total_amount number
createdAt timestamp
updatedAt timestamp
payment_status varchar(12) 
payment_mode enum["online" "COD"] not null
}

shipping[icon:truck]{
  shipping_id serial pk
  order_id  fk
  address_id fk
  shipping_date Date
  tracking_id varchar[24]
  createdAt timestamp
  updatedAt timestamp
}

customer.customer_id < orders.customer_id
product.product_id - order_item.product_id
orders.order_id < order_item.order_id
orders.order_id < shipping.order_id
orders.order_id < payment.order_id
customer.customer_id - address.customer_id
address.address_id - shipping.address_id


