doctors[icon:stethoscope, color: Orange]{
  doctor_id pk
  name string
  specialization enum [ "Cardiology","Pediatrics" ]
  experience years 
  work_history string
  consultation_fee number 
  clinic_name string
  clinic_address string
  preferred_by number
  createdAt timestamp
  updatedAt timestamp
}

patients[icon:user, color: Orange]{
  patient_id pk
  name string
  gender string
  DOB string 
  address string 
  phone number
  email string 
  is_active boolean
  diseases string
  blood_group string
  medical_history string
  lifestyle string
  createdAt timestamp
  updatedAt timestamp
}

appointments[icon:list, color: Orange]{
  appointment_id pk
  patient_id fk
  doctor_id fk
  time_slot date
  time_slot_expired date
  status enum ["booked", "cancelled", "completed"]
  createdAt timestamp
  updatedAt timestamp
}

consultations[icon:users, color: Orange]{
  consultation_id pk
  appointment_id fk
  prescription string
  createdAt timestamp
  updatedAt timestamp
}

diagnostics[icon:test-tube, color: Orange]{
  diagnostic_id pk
  patient_id fk
  doctor_id fk
  report_id fk
  symptoms string
  physical string
  createdAt timestamp
  updatedAt timestamp
}

reports[icon:report, color: Orange]{
  report_id pk
  patient_id fk
  doctor_id fk
  type enum ["lab", "imaging"]
  tests enum ["blood", "urine"]
  imaging enum ["x-ray", "MRI"]
  createdAt timestamp
  updatedAt timestamp
}

Medical_history[color: Orange]{
  history_id pk
  patient_id fk
  condition string
  description string
  createdAt timestamp
  updatedAt timestamp
}

payments[icon:rupee, color: Orange]{
  payment_id pk
  patient_id fk 
  appointment_id fk
  consultation_id fk
  doctor_id fk
  amount number
  createdAt timestamp
  updatedAt timestamp
}

patients.patient_id < appointments.patient_id
doctors.doctor_id < appointments.doctor_id
appointments.appointment_id - consultations.appointment_id
patients.patient_id < diagnostics.patient_id
doctors.doctor_id < diagnostics.doctor_id
reports.report_id - diagnostics.report_id
patients.patient_id < reports.patient_id
doctors.doctor_id < reports.doctor_id
patients.patient_id < payments.patient_id
appointments.appointment_id - payments.appointment_id
consultations.consultation_id - payments.consultation_id
doctors.doctor_id < payments.doctor_id
patients.patient_id < Medical_history.patient_id





