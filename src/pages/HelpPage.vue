<template>
  <f7-page name="help">
    <f7-navbar title="Довідка" back-link="Назад" />

    <div class="app-content">
      <div class="page-heading">
        <h1>Довідка</h1>
        <p>Правила використання TaskFlow</p>
      </div>

      <div class="info-card">
        <h3>Розділи застосунку</h3>
        <ul class="help-list">
          <li><b>Головна</b> — статистика (усього, виконано, очікує) та три останні завдання.</li>
          <li><b>Завдання</b> — повний список із назвою, описом і статусом.</li>
          <li><b>Про застосунок</b> — технології та версія TaskFlow.</li>
        </ul>
      </div>

      <div class="info-card">
        <h3>Позначення</h3>
        <div class="legend-row">
          <f7-icon f7="checkmark_circle_fill" class="completed-icon" />
          <span>завдання виконано</span>
        </div>
        <div class="legend-row">
          <f7-icon f7="circle" />
          <span>завдання очікує виконання</span>
        </div>
      </div>

      <div class="info-card">
        <h3>Встановлення</h3>
        <p>
          TaskFlow — PWA: у Chrome та Edge натисніть «Встановити» в адресному рядку,
          на Android та iPhone — «Додати на головний екран».
        </p>
      </div>

      <f7-button fill large back class="page-action">
        Повернутися
      </f7-button>
    </div>
  </f7-page>
</template>
