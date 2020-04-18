<template>
  <div 
    @click="$emit('taskStateChanged', task)"
    class="task" :class="stateClass">
    <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true }
  },
  computed: {
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending
      };
    }
  }
};
</script>

<style>
.task {
  position: relative;
  box-sizing: border-box;
  width: 350px;
  height: 100%;
  padding: 10px;
  border-radius: 3px;
  font-weight: 300;
  cursor: pointer;
  user-select: none;
  display: flex;
  justify-content: center;
  align-itens: center;
  color: #523c01;
}

.pending {
  line-height: 1;
  text-align:center;     
  width: 275px;    
  margin: 25px;    
  min-height:100px;
  max-height:250px;
  position:relative;   
  border:1px solid #E8E8E8;  
  font-size:1.5em;      
  border-bottom-right-radius: 60px 5px;
  display:inline-block;    
  background: #ffff88; /* Old browsers */
  background: -moz-linear-gradient(-45deg, #ffff88 81%, #ffff88 82%, #ffff88 82%, #ffffc6 100%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, right bottom, color-stop(81%,#ffff88), color-stop(82%,#ffff88), color-stop(82%,#ffff88), color-stop(100%,#ffffc6)); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(-45deg, #ffff88 81%,#ffff88 82%,#ffff88 82%,#ffffc6 100%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(-45deg, #ffff88 81%,#ffff88 82%,#ffff88 82%,#ffffc6 100%); /* Opera 11.10+ */
  background: -ms-linear-gradient(-45deg, #ffff88 81%,#ffff88 82%,#ffff88 82%,#ffffc6 100%); /* IE10+ */
  background: linear-gradient(135deg, #ffff88 81%,#ffff88 82%,#ffff88 82%,#ffffc6 100%); /* W3C */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffff88', endColorstr='#ffffc6',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */
}

.pending:after {     
  content: "";
  position:absolute;
  z-index:-1;
  right:-0px; bottom:20px;
  width:200px;
  height: 25px;
  background: rgba(0, 0, 0, 0.2);
  box-shadow:2px 15px 5px rgba(0, 0, 0, 0.40);
  -moz-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  -webkit-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  -o-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  -ms-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  transform: matrix(-1, -0.1, 0, 1, 0, 0);   
}

.done {
  text-decoration: line-through;
  line-height: 1;
  text-align:center;     
  width: 275px;    
  margin: 25px;    
  min-height:100px;
  max-height:250px;
  position:relative;   
  border:1px solid #94eb94;  
  font-size:1.5em;
  border-bottom-right-radius: 60px 5px;
  display:inline-block;    
  background: #7ef27e; /* Old browsers */
  background: -moz-linear-gradient(-45deg, #7ef27e 81%, #7ef27e 82%, #7ef27e 82%, #affaaf 100%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, right bottom, color-stop(81%,#7ef27e), color-stop(82%,#7ef27e), color-stop(82%,#7ef27e), color-stop(100%,#affaaf)); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(-45deg, #7ef27e 81%,#7ef27e 82%,#7ef27e 82%,#affaaf 100%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(-45deg, #7ef27e 81%,#7ef27e 82%,#7ef27e 82%,#affaaf 100%); /* Opera 11.10+ */
  background: -ms-linear-gradient(-45deg, #7ef27e 81%,#7ef27e 82%,#7ef27e 82%,#affaaf 100%); /* IE10+ */
  background: linear-gradient(135deg, #7ef27e 81%,#7ef27e 82%,#7ef27e 82%,#affaaf 100%); /* W3C */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#7ef27e', endColorstr='#affaaf',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */
}

.done:after{
  content: "";
  position:absolute;
  z-index:-1;
  right:-0px; bottom:20px;
  width:200px;
  height: 25px;
  background: rgba(0, 0, 0, 0.2);
  box-shadow:2px 15px 5px rgba(0, 0, 0, 0.40);
  -moz-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  -webkit-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  -o-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  -ms-transform: matrix(-1, -0.1, 0, 1, 0, 0);
  transform: matrix(-1, -0.1, 0, 1, 0, 0);   
}

.pending .close {
  background-color: #453303;

  
}

.done .close {
  background-color: #012b02;
}

.close {
  position: absolute;
  right: 10px;
  top: 10px;
  font-size: 0.9rem;
  font-weight: 600;
  height: 20px;
  width: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  color:#FFF;

  -webkit-box-shadow: 4px 5px 13px -2px rgba(0,0,0,0.79); 
  box-shadow: 4px 5px 13px -2px rgba(0,0,0,0.79);
}

.close:hover
{
  background-color:tomato;
}
</style>
