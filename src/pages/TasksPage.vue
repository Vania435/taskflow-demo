<template>
  <f7-page name="tasks">
    <f7-navbar title="Мої завдання" />

    <div class="app-content">
      <div class="page-heading">
        <h1>Завдання</h1>
        <p>Список поточних завдань</p>
      </div>

      <!-- Додаткове завдання 5: порожній список через v-if / v-else -->
      <div v-if="tasks.length" class="task-list">
        <div v-for="task in tasks" :key="task.id" class="task-row task-row-detail">
          <f7-icon
            :f7="task.completed ? 'checkmark_circle_fill' : 'circle'"
            :class="{ 'completed-icon': task.completed }"
          />
          <div class="task-details">
            <div class="task-title">{{ task.title }}</div>
            <div class="task-description">{{ task.description }}</div>
            <div class="task-status" :class="{ 'task-status-done': task.completed }">
              {{ task.completed ? 'Виконано' : 'Очікує виконання' }}
            </div>
          </div>
        </div>
      </div>
      <div v-else class="empty-state">
        <f7-icon f7="tray" />
        <p>Завдань поки немає</p>
      </div>

      <p class="helper-text">
        Створення, редагування та видалення завдань — у наступних заняттях.
      </p>
    </div>

    <AppTabbar active="tasks" />
  </f7-page>
</template>

<script setup>
import AppTabbar from '../components/AppTabbar.vue';
import { tasks } from '../data/tasks.js';
</script>
