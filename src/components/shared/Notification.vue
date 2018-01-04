<template>
  <div>
    <div class="container">
      <div class="colums">
        <div class="column is-5 is-offset-4">
          <div class="notification is-warning">
            <slot name="body">
              😥 No obtuvimos resultado, Intentalo de nuevo. 😎 🎵 📻 🚀
            </slot>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
