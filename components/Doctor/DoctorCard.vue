<template>
  <div class="bg-white rounded-xl shadow-md p-6 w-full max-w-[600px] mx-auto font-sans">
    <div class="flex items-center mb-6">
      <img src="../../assets/Images/doctor-avatar.svg" alt="Doctor Avatar"
        class="w-20 h-20 rounded-full mr-4 object-cover">
      <div class="flex-grow">
        <h2 class="text-xl font-medium text-gray-800 mb-1">{{ name }}</h2>
        <p class="text-sm text-gray-500">{{ specialization }}</p>
      </div>
    </div>
    <div class="mt-4">
      <div class="flex items-center mb-2 text-gray-700">
        <img src="../../assets/Images/phone.svg" alt="Phone Icon" class="w-5 h-5 mr-2 object-contain">
        <span class="text-sm">{{ contact.phone }}</span>
      </div>
      <div class="flex items-center mb-2 text-gray-700">
        <img src="../../assets/Images/email.svg" alt="Email Icon" class="w-5 h-5 mr-2 object-contain">
        <span class="text-sm">{{ contact.email }}</span>
      </div>
      <div class="flex items-center mb-2 text-gray-700">
        <img src="../../assets/Images/location.svg" alt="Location Icon" class="w-5 h-5 mr-2 object-contain">
        <span class="text-sm">{{ contact.address }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  name: {
    type: String,
    default: 'Dr. John Doe',
  },
  specialization: {
    type: String,
    default: 'General Practitioner',
  },
  contact: {
    type: Object,
    default: () => ({
      phone: '123-456-7890',
      email: 'john.doe@example.com',
      address: '123 Main Street, Anytown',
    }),
  },
});
</script>