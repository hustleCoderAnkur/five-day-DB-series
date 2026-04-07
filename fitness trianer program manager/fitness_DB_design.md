coach[color: Orange] {
coach_id serial pk
coach_name varchar(50)
gender enum ["male" "female"]
specialization enum ["fatloss" "weight gain"]
qualifications enum ["NONE" "BSC" "MSC" "CERT" ]
experience date
ratings number
certificate_image_url varchar(50)
bio text
createdat timestamp
updatedat timestamp
}

client[icon:user, color: Orange]{
client_id serial pk
client_name varchar(50)
fitness_goal varchar(20)
createdat timestamp
updatedat timestamp
}

subscriptions[icon: list, color: Orange]{
subscriptions_id serial pk
plan_id fk
client_id fk
payment_id fk
status ENUM ['active','completed','cancelled']
createdat timestamp
updatedat timestamp
}

plan [color: Orange]{
plan_id serial pk
plan_name varchar(50)
type enum ["fatloss" "weight gain"]
endGoal varchar(100)
price number
createdat timestamp
updatedat timestamp
}

consultations_scedule[icon:users, color: Orange]{
consultations_schedule_id serial pk
consulting_session_id fk
createdat timestamp
updatedat timestamp
}

consulting[icon:users, color: Orange]{
consulting_session_id serial pk
coach_id fk
client_id fk
start date
end date
type enum ["fatloss" "weight gain"]
consulation_name varchar(50)
price number
createdat timestamp
updatedat timestamp
}

progress[icon:user-md, color: Orange]{
progress_id serial pk
client_id fk
age number
weight number
hieght number
createdat timestamp
updatedat timestamp
}

payment[icon:rupee, color: Orange]{
payment_id serial pk
client_id fk
subscriptions_id fk
payment_date date
price number
status enum ['pending','paid','failed']
createdat timestamp
updatedat timestamp
}

consulting.consulting_session_id > consultations_scedule.consulting_session_id: [color: green]
plan.plan_id  > subscriptions.plan_id: [color: green]
client.client_id < subscriptions.client_id: [color: green]
progress.client_id - client.client_id: [color: green]
client.client_id - payment.client_id: [color: green]
consulting.coach_id - client.client_id: [color: green]
payment.payment_id < subscriptions.payment_id: [color: green]

coach.coach_id - client.client_id: [color: green]

