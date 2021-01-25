<script>
  export default {
    name: 'modal',
    methods: {
      close() {
        this.$emit('close');
      },
    },
  };
</script>
<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header
          class="modal-header"
          id="modalTitle"
        >
          <slot name="header">
            Add Movie

            <button
              type="button"
              class="btn-close"
              @click="close"
              aria-label="Close modal"
            >
              x
            </button>
          </slot>
        </header>
        <section
          class="modal-body"
          id="modalDescription"
        >
          <slot name="body">
           <div class="content" >
            <label for="Name">Name:</label>
           <input type="text" name="Name" placeholder="Add Movie Name" >
            
           </div>
             <div  class="content">
            <label>Summary:</label>
           <textarea type="text"  class="summary" placeholder="Add Movie Summary" ></textarea>
            
           </div>
             <div  class="upload">
            <label>Image:</label>
           <input type="file"  >
            
           </div>
           

          </slot>
        </section>
        <footer class="modal-footer">
          <slot name="footer">
            <button
              type="button"
              class="btn-green"
              @click="close"
              aria-label="Close modal"
            >
              Save
            </button>
        
            <button
              type="button"
              class="btn-red"
              @click="close"
              aria-label="Close modal"
            >
              Close me!
            </button>
          </slot>
        </footer>
      </div>
    </div>
  </transition>
</template>
<style>
input[type=submit] {
  width: auto !important;
  background-color: #4CAF50  !important;
  color: white;
  padding: 7px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
input[type=text]{
    width: 100%;
    padding: 5px 6px;
  margin: 6px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
.summary{
     width: 100%;
    padding: 5px 6px;
  margin: 6px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;

}
.content label{
    display: block;
}
.upload label{
    margin: 6px 0;
    display: block
}
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    border-bottom: 1px solid #eeeeee;
    color: #4AAE9B;
    justify-content: space-between;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 4px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
   width: auto;
  background-color: #4CAF50;
  color: white;
  padding: 8px 15px;
  margin: 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  }
  .btn-red {
   width: auto;
  background-color: red;
  color: white;
  padding: 8px 15px;
  margin: 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  }
</style>