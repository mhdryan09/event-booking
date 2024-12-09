<template>
  <main class="container mx-auto my-8 space-y-8">
    <h1 class="text-4xl">Event Booking App</h1>
    <h2 class="text-2xl font-medium">All Event</h2>
    <section class="grid grid-cols-2 gap-8">
      <template v-if="!eventsLoading">
        <EventCard
          v-for="event in events"
          :key="event.id"
          :title="event.title"
          :when="event.date"
          :description="event.description"
          @register="handleRegistration(event)"
        />
      </template>

      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i" />
      </template>
    </section>

    <h2 class="text-2xl font-medium">Your Bookings</h2>

    <section class="grid grid-cols-1 gap-4">
      <template v-if="!bookingsLoading">
        <BookingItem
          v-for="booking in bookings"
          :key="booking.id"
          :title="booking.eventTitle"
          :status="booking.status"
          @cancelled="cancelBooking(booking.id)"
        />
      </template>
      <template v-else>
        <LoadingBookingItem v-for="i in 3" :key="i" />
      </template>
    </section>
  </main>
</template>

<script setup>
import EventCard from '@/components/EventCard.vue';
import BookingItem from '@/components/BookingItem.vue';
import LoadingEventCard from '@/components/LoadingEventCard.vue';
import { ref, onMounted } from 'vue';
import LoadingBookingItem from '@/components/LoadingBookingItem.vue';

const events = ref([]);
const eventsLoading = ref(false);

const bookings = ref([]);
const bookingsLoading = ref(false);

const fetchEvents = async () => {
  eventsLoading.value = true;
  try {
    const response = await fetch('http://localhost:3001/events');
    events.value = await response.json();
  } catch (error) {
    console.log(error, 'error');
  } finally {
    eventsLoading.value = false;
  }
};

const fetchBookings = async () => {
  bookingsLoading.value = true;
  try {
    const response = await fetch('http://localhost:3001/bookings');
    bookings.value = await response.json();
  } catch (error) {
    console.log(error, 'error');
  } finally {
    bookingsLoading.value = false;
  }
};

const findBookingById = (id) => {
  bookings.value.findIndex((booking) => booking.id === id);
};

const handleRegistration = async (event) => {
  // cek apakah user sudah terdaftar di event ini
  // cek id event dan id user
  if (bookings.value.some((booking) => booking.eventId === event.id && booking.userId === 1)) {
    alert('You have already registered for this event');
    return;
  }

  const newBooking = {
    id: Date.now().toString(),
    userId: 1,
    eventId: event.id,
    eventTitle: event.title,
    status: 'pending'
  };

  // add booking to the array
  bookings.value.push(newBooking);

  try {
    const response = await fetch('http://localhost:3001/bookings', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        ...newBooking,
        status: 'confirmed'
      })
    });

    if (response.ok) {
      // find index
      const index = findBookingById(newBooking.id);

      // update status
      // bookings.value[index]
      bookings.value[index] = await response.json();
    } else {
      throw new Error('failed to confirm booking');
    }
  } catch (error) {
    console.error(`Failed to register for event : `, error);
    bookings.value = bookings.value.filter((booking) => booking.id !== newBooking.id);
    // hapus dari array bookings karena gagal register
  }
};

const cancelBooking = async (bookingId) => {
  const index = findBookingById(bookingId);
  const originalBooking = bookings.value[index]; // simpan booking sebelumnya sebelum dihapus
  bookings.value.splice(index, 1); // hapus dari array bookings

  try {
    const response = await fetch(`http://localhost:3001/bookings/${bookingId}`, {
      method: 'DELETE'
    });

    if (!response.ok) {
      throw new Error('Booking could not be cancelled');
    }
  } catch (error) {
    console.error('Failed to cancel booking', error);
    bookings.value.splice(index, 0, originalBooking); // kembalikan ke array bookings sebelumnya jika cancel booking gagal
  }
};

onMounted(() => {
  fetchEvents();
  fetchBookings();
});
</script>
