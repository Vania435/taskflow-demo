<script setup>
import { computed, ref } from 'vue'
import AppTabbar from '../components/AppTabbar.vue'
import TaskCard from '../components/TaskCard.vue'
import TaskCounter from '../components/TaskCounter.vue'
import { taskState, setTaskStatus, setTaskPriority, priorityOrder } from '../store/tasks'
import '../css/task-components.css'

const totalTasks = computed(() => taskState.tasks.length)
const completedTasks = computed(() => taskState.tasks.filter((task) => task.status === 'done').length)
const progressTasks = computed(() => taskState.tasks.filter((task) => task.status === 'progress').length)
// Додаткове завдання 2: четвертий показник «Заплановано»
const plannedTasks = computed(() => taskState.tasks.filter((task) => task.status === 'todo').length)
// Додаткове завдання 4: відсоток виконаних завдань
const completedPercent = computed(() => (
  totalTasks.value ? Math.round((completedTasks.value / totalTasks.value) * 100) : 0
))

const activeTasks = computed(() => taskState.tasks
  .filter((task) => task.status !== 'done')
  .sort((a, b) => priorityOrder[a.priority] - priorityOrder[b.priority])
  .slice(0, 3))

const selectedTitle = ref('')

function handleStatusChange(payload) { setTaskStatus(payload) }
function handlePriorityChange(payload) { setTaskPriority(payload) }
function handleTaskSelect(payload) { selectedTitle.value = payload.title }
</script>

<template>
  <f7-page name="home" class="tf3-page">
    <f7-navbar title="TaskFlow">
      <f7-nav-right>
        <f7-link href="/about/" aria-label="Про застосунок">Про застосунок</f7-link>
      </f7-nav-right>
    </f7-navbar>

    <div class="tf3-container">
      <section class="tf3-hero">
        <div class="tf3-eyebrow">TASKFLOW / DASHBOARD</div>
        <h1>Панель керування</h1>
        <p>Контролюйте виконання завдань та їхні пріоритети.</p>
      </section>

      <section class="tf3-stat-grid tf3-stat-grid--four">
        <TaskCounter label="Усього завдань" :value="totalTasks" />
        <TaskCounter label="Заплановано" :value="plannedTasks" accent="todo" />
        <TaskCounter label="У роботі" :value="progressTasks" accent="progress" />
        <TaskCounter label="Виконано" :value="completedTasks" accent="done" />
      </section>

      <section class="tf3-progress" aria-label="Відсоток виконаних завдань">
        <div class="tf3-progress-head">
          <span>Виконано завдань</span>
          <strong>{{ completedPercent }}%</strong>
        </div>
        <div class="tf3-progress-track">
          <div class="tf3-progress-bar" :style="{ width: `${completedPercent}%` }" />
        </div>
      </section>

      <section class="tf3-section">
        <div class="tf3-section-heading">
          <div>
            <div class="tf3-eyebrow">PRIORITY TASKS</div>
            <h2>Актуальні завдання</h2>
          </div>
          <f7-button href="/tasks/" outline small>Переглянути всі</f7-button>
        </div>

        <div v-if="selectedTitle" class="tf3-selected">
          Обране завдання: <strong>{{ selectedTitle }}</strong>
        </div>

        <div v-if="activeTasks.length" class="tf3-task-grid">
          <TaskCard
            v-for="task in activeTasks"
            :key="task.id"
            :task="task"
            :selected="task.title === selectedTitle"
            @status-change="handleStatusChange"
            @priority-change="handlePriorityChange"
            @task-select="handleTaskSelect"
          />
        </div>
        <div v-else class="tf3-empty">Наразі всі завдання виконані.</div>
      </section>
    </div>

    <AppTabbar active="home" />
  </f7-page>
</template>
