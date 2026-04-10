buildings[color: Orange]{
  building_id pk
  name string
  address string
  city string
  type enum ["corporate" "mall" "airport" "hospital"]
  total_floors number
  created_at timestamp
  updated_at timestamp
}

floors[color: Orange]{
  floor_id pk
  building_id fk
  floor_number number
  created_at timestamp
  updated_at timestamp
}

elevator_shafts[color: Orange]{
  shaft_id pk
  building_id fk
  shaft_code string
  created_at timestamp
  updated_at timestamp
}

elevators[color: Orange]{
  elevator_id pk
  shaft_id fk
  building_id fk
  name string
  capacitance number
  manufactured_by string
  installed_at timestamp
  created_at timestamp
  updated_at timestamp
}

elevator_status[color: Orange]{
  status_id pk
  elevator_id fk
  current_status enum ["up" "down" "maintenance" "disabled"]
  current_floor_id fk
  created_at timestamp
  updated_at timestamp
}

floor_requests[color: Orange]{
  request_id pk
  floor_id fk
  building_id fk
  direction enum ["up" "down"]
  requested_at timestamp
  status enum ["pending" "completed" "cancelled"]
  created_at timestamp
  updated_at timestamp
}

ride_assignments[color: Orange]{
  assignment_id pk
  request_id fk
  elevator_id fk
  created_at timestamp
  updated_at timestamp
  status enum ["progress" "completed" "failed"]
}

ride[color: Orange]{
  ride_id pk
  assignment_id fk
  elevator_id fk
  floor_id fk
  started_at timestamp
  completed_at timestamp
  duration number
  count number
}

maintenance_logs[color: Orange]{
  maintenance_id pk
  elevator_id fk
  reported_by string
  type enum ["routine" "breakdown" "inspection" "repair"]
  description string
  status enum ["scheduled" "progress" "completed"]
  reported_at timestamp
  updated_at timestamp
  completed_at timestamp
}

buildings.building_id < floors.building_id: [color: green]
buildings.building_id < elevator_shafts.building_id: [color: green]
buildings.building_id < elevators.building_id: [color: green]
buildings.building_id < floor_requests.building_id: [color: green]

elevator_shafts.shaft_id - elevators.shaft_id: [color: green]

elevators.elevator_id - elevator_status.elevator_id: [color: green]
elevators.elevator_id < ride_assignments.elevator_id: [color: green]
elevators.elevator_id < ride.elevator_id: [color: green]
elevators.elevator_id < maintenance_logs.elevator_id: [color: green]

floors.floor_id < elevator_status.current_floor_id: [color: green]
floors.floor_id < floor_requests.floor_id: [color: green]
floors.floor_id < ride.floor_id: [color: green]

floor_requests.request_id - ride_assignments.request_id: [color: green]

ride_assignments.assignment_id - ride.assignment_id: [color: green]