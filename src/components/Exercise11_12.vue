<template>
    <div id="todo-list">
      <h3>Danh sách công việc</h3>
      <div id="todo-input-container">
        <input
          v-model="nameJob"
          type="text"
          id="todo-input"
          placeholder="Nhập tên công việc"
        />
        <button v-if="!checkUpdate" @click="handleAdd" id="add-button">Thêm</button>
        <button v-else @click="updateJob" id="add-button">Edit</button>
      </div>
  
      <ul id="tasks-list">
        <li v-for="job in listJobs" :key="job.id" class="task-item">
          <input
            type="checkbox"
            class="task-checkbox"
            :checked="job.status"
            @change="toggleJobStatus(job.id)"
          />
          <label :class="{ completed: job.status }">{{ job.name }}</label>
          <div class="task-actions">
            <button @click="handleEdit(job.id)" class="edit-button">✏️</button>
            <button @click="deleteButton(job.id)" class="delete-button">🗑️</button>
          </div>
        </li>
      </ul>
  
      <p id="task-counter">Công việc đã hoàn thành: {{ jobComplete }} / {{ listJobs.length }}</p>
    </div>
  </template>
  
  <script setup>
  import { reactive, ref, watch } from "vue";
  
  const nameJob = ref("");
  const listJobs = ref(JSON.parse(localStorage.getItem("data")));
  const editingJobId = ref(null);
  const checkUpdate = ref(false);
  const jobComplete = ref(0);
  const updateJobComplete = () => {
    jobComplete.value = listJobs.value.filter((job) => job.status === true).length;
  };
  updateJobComplete();
  
  const handleAdd = () => {
    const find = listJobs.value.find((job) => job.name === nameJob.value);
    if (!find) {
      const newJob = {
        id: listJobs.value.length + 1,
        name: nameJob.value,
        status: false,
      };
      listJobs.value.push(newJob);
      localStorage.setItem("data", JSON.stringify(listJobs.value));
      nameJob.value = ""; 
    }
  };
  
  const deleteButton = (id) => {
    listJobs.value = listJobs.value.filter((job) => job.id !== id);
    localStorage.setItem("data", JSON.stringify(listJobs.value));
    updateJobComplete();
  };
  
  const handleEdit = (id) => {
    const job = listJobs.value.find((job) => job.id === id);
    if (job) {
      nameJob.value = job.name;
      checkUpdate.value = true;
      editingJobId.value = id;
    }
  };
  
  const updateJob = () => {
    const jobIndex = listJobs.value.findIndex((job) => job.id === editingJobId.value);
    if (jobIndex !== -1) {
      listJobs.value[jobIndex].name = nameJob.value;
      localStorage.setItem("data", JSON.stringify(listJobs.value));
      nameJob.value = "";
      checkUpdate.value = false;
      editingJobId.value = null;
    }
  };
  
  const toggleJobStatus = (id) => {
    const jobIndex = listJobs.value.findIndex((job) => job.id === id);
    if (jobIndex !== -1) {
      listJobs.value[jobIndex].status = !listJobs.value[jobIndex].status; 
      localStorage.setItem("data", JSON.stringify(listJobs.value));
      updateJobComplete(); 
    }
  };
  </script>
  
  <style>
  #todo-list {
    margin-top: 20px;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  h3 {
    text-align: center;
    color: #333;
    font-size: 24px;
    margin-bottom: 20px;
  }
  
  #todo-input-container {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }
  
  #todo-input {
    width: 75%;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
    outline: none;
    transition: border-color 0.3s ease;
  }
  
  #todo-input:focus {
    border-color: #007bff;
  }
  
  #add-button {
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;
  }
  
  #add-button:hover {
    background-color: #0056b3;
  }
  
  #tasks-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  
  .task-item {
    display: flex;
    align-items: center;
    padding: 10px;
    background-color: white;
    border-radius: 5px;
    margin-bottom: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease;
  }
  
  .task-item:hover {
    transform: translateY(-2px);
  }
  
  .task-checkbox {
    margin-right: 15px;
    width: 18px;
    height: 18px;
  }
  
  label {
    font-size: 16px;
    flex-grow: 1;
    color: #333;
  }
  
  label.completed {
    text-decoration: line-through;
    color: #999;
  }
  
  .task-actions {
    display: flex;
    gap: 10px;
  }
  
  .task-actions button {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 18px;
    color: #555;
    transition: color 0.3s ease;
  }
  
  .task-actions button:hover {
    color: #007bff;
  }
  
  #task-counter {
    margin-top: 20px;
    font-weight: bold;
    text-align: center;
    font-size: 16px;
    color: #555;
  }
  </style>
  