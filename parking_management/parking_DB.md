vehicles[color: Orange]{
vehicle_id pk
vehicle_categories_id fk
vehicle_number string
owner_name string
owner_mob_number number
owner_email string
}

vehicle_categories[color: Orange]{
vehicle_categories_id pk 
type enum ["bikes" "cars" "SUVs" "cabs" "EV"]
createdat timestamp
updatedat timestamp
}

parking_spots[color: Orange]{
  spot_id pk
  serial_number number
  spot_category_id fk
  zone_id fk
  created_at timestamp
  updated_at timestamp
}

parking_spot_categories[color: Orange]{
spot_categories pk
type enum ["public", "reserved"]
}

parking_zones[color: Orange]{
zone_id pk
type enum ["level_1" "level_2" "level_3"]
createdat timestamp
updatedat timestamp
}

parking_tickets[color: Orange]{
  ticket_id pk
  session_id fk
  payment_id fk
  issued_at timestamp
}

reservations[color: Orange]{
  reservation_id pk
  vehicle_id fk
  spot_id fk
  reserved_from timestamp
  reserved_until timestamp
  status enum ["upcoming" "active" "cancelled" "expired"]
  created_at timestamp
}

parking_sessions[color: Orange, styleMode: plain]{
  session_id pk
  vehicle_id fk
  spot_id fk
  entry_time timestamp
  exit_time timestamp
  status enum ["active","completed"]
  created_at timestamp
  updated_at timestamp
}

payments[color: Orange]{
payment_id pk
amount number 
status enum ["failed" "pending" "successful"]
payment_method enum ["online" "cash" ]
createdat timestamp
updatedat timestamp
}

vehicles.vehicle_id < parking_sessions.vehicle_id: [color: green]
parking_spots.spot_id <> parking_sessions.spot_id: [color: green]
parking_spot_categories.spot_categories < parking_spots.spot_category_id: [color: green]
parking_zones.zone_id <> parking_spots.zone_id: [color: green]
vehicle_categories.vehicle_categories_id < vehicles.vehicle_categories_id: [color: green]
parking_sessions.session_id < parking_tickets.session_id: [color: green]
payments.payment_id > parking_tickets.payment_id: [color: green]
reservations.vehicle_id > vehicles.vehicle_id: [color: green]
reservations.spot_id > parking_spots.spot_id: [color: green]



