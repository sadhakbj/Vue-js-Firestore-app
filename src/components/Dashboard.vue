<template>
    <div id="dashboard">
        <ul class="collection with-header">
            <li class="collection-header">
                <h4>Employees List</h4>
                <div class="preloader-wrapper big active" v-if="!loaded">
                    <div class="spinner-layer spinner-blue-only">
                        <div class="circle-clipper left">
                            <div class="circle"></div>
                        </div>
                        <div class="gap-patch">
                            <div class="circle"></div>
                        </div>
                        <div class="circle-clipper right">
                            <div class="circle"></div>
                        </div>
                    </div>
                </div>
            </li>
            <li v-for="employee in employees" :key="employee.id" class="collection-item">
                <div class="chip">{{ employee.department }}</div>
                {{ employee.employee_id }}: {{ employee.name }}
                <router-link class="secondary-content" :to="{ name: 'view-employee', params: { employee_id: employee.employee_id }}"><i class="fa fa-eye"></i></router-link>
    
            </li>
        </ul>
        <div class="fixed-action-btn">
            <router-link to="/new" class="btn-floating btn-large red"> <i class="fa fa-plus"></i> </router-link>
        </div>
    </div>
</template>

<script>
    import db from './firebaseInit'
    export default {
        name: 'dashboard',
        data() {
            return {
                loaded: false,
                employees: []
            }
        },
        created() {
            this.loaded = false
            db.collection('employees').orderBy('dept').get().then(querySnapshot => {
                querySnapshot.forEach(doc => {
                    const data = {
                        'id': doc.id,
                        'employee_id': doc.data().employee_id,
                        'name': doc.data().name,
                        'department': doc.data().dept,
                        'position': doc.data().position
                    };
                    this.employees.push(data);
                    this.loaded = true
                })
            })
        }
    }
</script>
