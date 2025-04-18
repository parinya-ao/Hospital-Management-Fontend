<template>
  <div class="min-h-screen bg-blue-50 p-6">
    <div class="bg-white p-6 rounded-lg shadow-md">
      <h1 class="text-2xl font-bold text-blue-900">ข้อมูลผู้ป่วย</h1>
    </div>

    <div v-if="patient" class="bg-white p-6 mt-4 rounded-lg shadow-md">
      <h2 class="text-xl font-semibold">{{ patient.name }}</h2>
      <p class="text-sm text-gray-600">อายุ: {{ patient.age }}</p>
      <p class="text-sm text-gray-600">เพศ: {{ patient.gender }}</p>

      <!-- Contact Information -->
      <div class="mt-4">
        <h3 class="text-lg font-semibold text-gray-700">ข้อมูลติดต่อ</h3>
        <p class="text-sm text-gray-600">📞 โทรศัพท์: {{ patient.contact.phone }}</p>
        <p class="text-sm text-gray-600">📧 อีเมล: {{ patient.contact.email }}</p>
        <p class="text-sm text-gray-600">📍 ที่อยู่: {{ patient.contact.address }}</p>
      </div>

      <!-- Medical History -->
      <div class="mt-4">
        <h3 class="text-lg font-semibold text-gray-700">ประวัติทางการแพทย์</h3>
        <ul>
          <li
            v-for="(record, index) in patient.medical_history"
            :key="index"
            class="p-2 border-b"
          >
            <strong>{{ record.disease }}</strong> 
            <br> 🗓️ วันที่วินิจฉัย: {{ record.diagnosed_date }} 
            <br> 💊 การรักษา: {{ record.treatment }}
          </li>
        </ul>
      </div>

      <!-- Appointments -->
      <div class="mt-4">
        <h3 class="text-lg font-semibold text-gray-700">การนัดหมาย</h3>
        <ul>
          <li
            v-for="(appointment, index) in patient.appointments"
            :key="index"
            class="p-2 border-b"
          >
            <strong>🗓️ วันที่: {{ appointment.date }}</strong>
            <br> ⏰ เวลา: {{ appointment.time }}
            <br> 📍 สถานที่: {{ appointment.location }}
          </li>
        </ul>
        <p v-if="patient.appointments.length === 0" class="text-sm text-gray-500">ไม่มีการนัดหมาย</p>
      </div>

      <!-- Prescriptions -->
      <div class="mt-4">
        <h3 class="text-lg font-semibold text-gray-700">ใบสั่งยา</h3>
        <ul>
          <li
            v-for="(prescription, index) in patient.prescriptions"
            :key="index"
            class="p-2 border-b"
          >
            <strong>💊 ยา: {{ prescription.medicine }}</strong>
            <br> 🕒 ปริมาณ: {{ prescription.dosage }}
            <br> 📋 หมายเหตุ: {{ prescription.notes }}
          </li>
        </ul>
        <p v-if="patient.prescriptions.length === 0" class="text-sm text-gray-500">ไม่มีใบสั่งยา</p>
      </div>
    </div>
    
    <div v-else class="text-center p-6">กำลังโหลดข้อมูลผู้ป่วย...</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const patient = ref(null);

const fetchPatientDetails = async () => {
  try {
    const response = await fetch(`http://127.0.0.1:8000/patients/get/${route.params.id}`);
    if (response.ok) {
      patient.value = await response.json();
    } else {
      console.error("Patient not found");
    }
  } catch (error) {
    console.error("Error fetching patient data:", error);
  }
};

onMounted(fetchPatientDetails);
</script>
