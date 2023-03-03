<template>
    {{ msg }}
    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Update</th>
                <th>Delete</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="val, i in todoData" v-bind:key="i">
                <td>{{ val }}</td>
                <td><button @click="UpdateMe(i)">Update</button></td>
                <td><button @click="DeleteMe(i)">Delete</button></td>
            </tr>
        </tbody>
    </table>
    <div>
        <input type="text" name="fanme" v-model="formData.fname" />
        <button @click="dataUpdation()">{{ (updatebtn)? 'Update':'Add' }}</button>
        
    </div>
</template>
<script>
export default {
  name: 'TodoTemplate',
  props: {
    msg: String
  },
  data(){
    return{
        todoData: [],
        formData: {},
        updatebtn: false,
        indexCache: null
    }
  },
  methods:{
    dataUpdation(){
        if(this.updatebtn){ 
            this.todoData[this.indexCache] = this.formData.fname;
            this.updatebtn= false;
        }else{
            this.formData.fname && this.todoData.push(this.formData.fname);
        }
        this.formData = {}
    },
    UpdateMe( i ){
     this.formData.fname = this.todoData[i];
     this.updatebtn = true
     this.indexCache = i;
    },
    DeleteMe( i ){
        this.todoData.splice(i, 1);
    }
  }
}
</script>