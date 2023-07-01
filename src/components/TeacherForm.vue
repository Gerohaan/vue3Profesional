<template>
   <section>
    <h3>Añadir profesor</h3>
    <div>
        <label for="">
            Nombre:
            <input type="text" v-model="teacher.teacherName"/>
        </label>
    </div>
    <div>
        <label for="">
            Apellidos:
            <input type="text" v-model="teacher.surname"/>
        </label>
    </div>
    <div>
        <label for="">
            DNI/ NIF:
            <input type="text" v-model="teacher.dni"/>
        </label>
    </div>
    
    <div>
        <label for="">
            Materias:
            <input type="text" v-model="subject"/><button @click="handleSubject()">Agregar</button>
        </label>
    </div>
    <div>
        <ul>
           <li v-for="(elm, index) in teacher.subjects" :key="index">
            {{ elm }}
            </li> 
        </ul>
    </div>
    <input type="checkbox" v-model="teacher.doc"/>Documentación entragada
    <button @click="handleAddTeacher()">Agregar</button>
   </section>

   <section>
    <h3>Listado de profesores</h3>
    <table>
        <tr>
            <th>Nombre</th>
            <th>Apellidos</th>
            <th>DNI / NIF</th>
            <th>Materias</th>
            <th>Documentación Entregada</th>
        </tr>
        <tr v-for="(item, index) in teachers" :key="index">
            <td>{{ item.teacherName }}</td>
            <td>{{ item.surname }}</td>
            <td>{{ item.dni }}</td>
            <td>{{ item.subjects }}</td>
            <td>{{ item.doc }}</td>
        </tr>
    </table>
   </section>
</template>

<script setup lang="ts">
import { Ref, ref } from 'vue'

interface ITeacher {
    teacherName: string,
    surname: string,
    dni: string,
    subjects: Array<string>,
    doc: boolean
}

let teacher:Ref<ITeacher> = ref({
    teacherName: '',
    surname: '',
    dni: '',
    subjects: [],
    doc: false
})

let teachers:Ref<Array<ITeacher>> = ref([])

let subject:Ref<string> = ref('')

const handleSubject = () => {
    teacher.value.subjects.push(subject.value)
    subject.value = ""
}

const handleAddTeacher = () => {
    teachers.value.push({
        teacherName: teacher.value.teacherName,
        surname: teacher.value.surname,
        dni: teacher.value.dni,
        subjects: teacher.value.subjects,
        doc: teacher.value.doc
    })
    teacher.value.teacherName = ""
    teacher.value.surname = ""
    teacher.value.dni = ""
    teacher.value.subjects = []
    teacher.value.doc = false
}


</script>

<style scoped>

</style>