<template>
    <v-app>
      <v-container>
        <v-row justify="center">
          <v-col cols="12" md="8">
            <v-text-field
              v-model="newTask"
              label="Yeni Görev Ekle"
              @keyup.enter="addTask"
              outlined
            ></v-text-field>
            <v-text-field
              v-model="newEmoji"
              label="Emoji Ekle (örn: 😎)"
              outlined
              class="mt-2"
            ></v-text-field>
            <v-btn @click="addTask" color="primary" class="mt-2 rounded-btn">
              Ekle
            </v-btn>
          </v-col>
        </v-row>
        <v-row justify="center">
          <v-col cols="12" md="8">
            <v-btn @click="completeAllTasks" color="success" class="mb-2 rounded-btn">
              Tümünü Tamamla
            </v-btn>
            <v-btn @click="clearCompletedTasks" color="error" class="mb-2 ml-2 rounded-btn">
              Tamamlananları Temizle
            </v-btn>
            <v-btn @click="deleteAllTasks" color="error" class="mb-2 ml-2 rounded-btn">
              Tüm Görevleri Sil
            </v-btn>
            <v-btn @click="shuffleTasks" color="info" class="mb-2 ml-2 rounded-btn">
              Görevleri Karıştır
            </v-btn>
            <v-btn @click="markSelectedImportantTasks" color="warning" class="mb-2 ml-2 rounded-btn">
              Seçili Görevleri Önemli Yap
            </v-btn>
            <v-btn @click="sortTasksByCompletion" color="primary" class="mb-2 ml-2 rounded-btn">
              Tamamlananlara Göre Sırala
            </v-btn>
            <v-btn @click="reverseTaskOrder" color="secondary" class="mb-2 ml-2 rounded-btn">
              Görev Sırasını Tersine Çevir
            </v-btn>
            <v-btn @click="removeImportantMarks" color="dark" class="mb-2 ml-2 rounded-btn">
              Önemli İşaretleri Kaldır
            </v-btn>
            <v-btn @click="highlightCompletedTasks" color="teal" class="mb-2 ml-2 rounded-btn">
              Tamamlananları Vurgula
            </v-btn>
            <v-btn @click="filterImportantTasks" color="amber" class="mb-2 ml-2 rounded-btn">
              Sadece Önemli Görevleri Göster
            </v-btn>
            <v-btn @click="showAllTasks" color="blue" class="mb-2 ml-2 rounded-btn">
              Tüm Görevleri Göster
            </v-btn>
            <v-btn @click="archiveCompletedTasks" color="brown" class="mb-2 ml-2 rounded-btn">
              Tamamlananları Arşivle
            </v-btn>
            <v-btn @click="pinTaskOrder" color="indigo" class="mb-2 ml-2 rounded-btn">
              Görev Sırasını Sabitle
            </v-btn>
            <v-btn @click="colorCodeTasks" color="lime" class="mb-2 ml-2 rounded-btn">
              Görevleri Renk Kodla
            </v-btn>
            <v-btn @click="setTaskReminder" color="blue darken-4" class="mb-2 ml-2 rounded-btn">
              Görev Hatırlatıcı Ayarla
            </v-btn>
            <v-btn @click="groupTasksByCategory" color="purple darken-3" class="mb-2 ml-2 rounded-btn">
              Görevleri Kategorilere Ayır
            </v-btn>
            <v-btn @click="highlightImportantTasks" color="pink darken-2" class="mb-2 ml-2 rounded-btn">
              Önemli Görevleri Vurgula
            </v-btn>
            <v-btn @click="sortByDueDate" color="green darken-3" class="mb-2 ml-2 rounded-btn">
              Bitiş Tarihine Göre Sırala
            </v-btn>
            <v-btn @click="exportTasksToJSON" color="orange darken-2" class="mb-2 ml-2 rounded-btn">
              Görevleri JSON Olarak Kaydet
            </v-btn>
            <v-btn @click="importTasksFromJSON" color="cyan darken-2" class="mb-2 ml-2 rounded-btn">
              JSON'dan Görev Yükle
            </v-btn>
            <v-btn @click="duplicateTask" color="red darken-3" class="mb-2 ml-2 rounded-btn">
              Seçili Görevi Çoğalt
            </v-btn>
            <v-btn @click="addRecurringTask" color="purple" class="mb-2 ml-2 rounded-btn">
              Yinelenen Görev Ekle
            </v-btn>
            <v-btn @click="showTasksWithReminder" color="grey" class="mb-2 ml-2 rounded-btn">
              Hatırlatıcı Ayarlanmış Görevleri Göster
            </v-btn>
            <v-btn @click="markTasksAsUrgent" color="red accent-4" class="mb-2 ml-2 rounded-btn">
              Seçili Görevleri Acil Yap
            </v-btn>
            <v-btn @click="addDeadline" color="deep-purple" class="mb-2 ml-2 rounded-btn">
              Son Tarih Ekle
            </v-btn>
            <v-btn @click="assignTasksToCategory" color="green darken-2" class="mb-2 ml-2 rounded-btn">
              Görevleri Belirli Kategorilere Ata
            </v-btn>
            <v-btn @click="toggleTaskVisibility" color="blue accent-4" class="mb-2 ml-2 rounded-btn">
              Görev Görünürlüğünü Değiştir
            </v-btn>
            <v-btn @click="setPriorityLevels" color="pink accent-3" class="mb-2 ml-2 rounded-btn">
              Görev Öncelik Seviyesi Belirle
            </v-btn>
            <v-btn @click="generateWeeklyReport" color="yellow darken-3" class="mb-2 ml-2 rounded-btn">
              Haftalık Rapor Oluştur
            </v-btn>
            <v-btn @click="addCustomLabels" color="teal lighten-1" class="mb-2 ml-2 rounded-btn">
              Özel Etiket Ekle
            </v-btn>
            <v-btn @click="assignMultipleTasks" color="purple darken-1" class="mb-2 ml-2 rounded-btn">
              Birden Fazla Görevi Ata
            </v-btn>
            <v-btn @click="trackTaskProgress" color="brown lighten-1" class="mb-2 ml-2 rounded-btn">
              Görev İlerlemesini Takip Et
            </v-btn>
            <v-btn @click="archiveOldTasks" color="deep-orange" class="mb-2 ml-2 rounded-btn">
              Eski Görevleri Arşivle
            </v-btn>
            <v-btn @click="shareTaskList" color="cyan accent-4" class="mb-2 ml-2 rounded-btn">
              Görev Listesini Paylaş
            </v-btn>
            <v-btn @click="copyTaskLink" color="light-green" class="mb-2 ml-2 rounded-btn">
              Görev Bağlantısını Kopyala
            </v-btn>
            <v-btn @click="setTaskColor" color="amber" class="mb-2 ml-2 rounded-btn">
              Göreve Renk Belirle
            </v-btn>
            <v-btn @click="sortByPriority" color="orange darken-4" class="mb-2 ml-2 rounded-btn">
              Önceliğe Göre Sırala
            </v-btn>
            <v-btn @click="markAsBlocked" color="blue-grey" class="mb-2 ml-2 rounded-btn">
              Görevi Engellendi Olarak İşaretle
            </v-btn>
            <v-btn @click="duplicateSelectedTasks" color="red darken-1" class="mb-2 ml-2 rounded-btn">
              Seçili Görevleri Çoğalt
            </v-btn>
            <v-btn @click="linkTasks" color="indigo darken-2" class="mb-2 ml-2 rounded-btn">
              Görevleri Birbirine Bağla
            </v-btn>
            <v-btn @click="addCompletionTime" color="lime darken-3" class="mb-2 ml-2 rounded-btn">
              Tamamlama Süresi Ekle
            </v-btn>
            <draggable v-model="tasks" @end="saveTasks">
              <template #item="{ element, index }">
                <v-list-item :key="index" :class="{ important: element.important }">
                  <v-list-item-content>
                    <v-list-item-title :class="{ done: element.completed }">
                      <v-checkbox v-model="element.selected" class="mr-3"></v-checkbox>
                      {{ element.emoji }} {{ element.text }}
                    </v-list-item-title>
                    <v-list-item-subtitle class="task-date">
                      Eklenme Tarihi: {{ element.createdAt }} | #{{ index + 1 }}
                    </v-list-item-subtitle>
                    <v-menu v-model="element.dueDateMenu" close-on-content-click="false" transition="scale-transition" offset-y>
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="element.dueDate"
                          label="Bitiş Tarihi (dd/mm/yyyy)"
                          prepend-icon="mdi-calendar"
                          placeholder="Örnek: 19/10/2024"
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="element.dueDate" @input="element.dueDateMenu = false" :min="new Date().toISOString().substr(0, 10)"></v-date-picker>
                    </v-menu>
                  </v-list-item-content>
                  <v-list-item-action>
                    <v-btn icon @click.stop="removeTask(index)">
                      <v-icon color="red">mdi-delete</v-icon>
                    </v-btn>
                  </v-list-item-action>
                </v-list-item>
              </template>
            </draggable>
          </v-col>
        </v-row>
      </v-container>
    </v-app>
  </template>
  
  <script>
  import draggable from "vuedraggable";
  
  export default {
    name: "TodoList",
    components: {
      draggable,
    },
    data() {
      return {
        newTask: "",
        newEmoji: "",
        tasks: [],
        tasksVisible: true,
      };
    },
    created() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks);
      }
    },
    methods: {
      addTask() {
        if (this.newTask.trim() === "") return;
  
        const currentDate = new Date().toLocaleDateString("tr-TR");
        this.tasks.push({
          text: this.newTask,
          emoji: this.newEmoji,
          completed: false,
          important: false,
          selected: false,
          createdAt: currentDate,
          dueDate: null,
          dueDateMenu: false,
          recurring: false,
        });
        this.newTask = "";
        this.newEmoji = "";
        this.saveTasks();
      },
      removeTask(index) {
        this.tasks.splice(index, 1);
        this.saveTasks();
      },
      saveTasks() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      completeAllTasks() {
        this.tasks.forEach((task) => {
          task.completed = true;
        });
        this.saveTasks();
      },
      clearCompletedTasks() {
        this.tasks = this.tasks.filter((task) => !task.completed);
        this.saveTasks();
      },
      deleteAllTasks() {
        this.tasks = [];
        this.saveTasks();
      },
      shuffleTasks() {
        this.tasks = this.tasks.sort(() => Math.random() - 0.5);
        this.saveTasks();
      },
      markSelectedImportantTasks() {
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.important = true;
          }
        });
        this.saveTasks();
      },
      sortTasksByCompletion() {
        this.tasks.sort((a, b) => a.completed - b.completed);
        this.saveTasks();
      },
      reverseTaskOrder() {
        this.tasks.reverse();
        this.saveTasks();
      },
      removeImportantMarks() {
        this.tasks.forEach((task) => {
          task.important = false;
        });
        this.saveTasks();
      },
      highlightCompletedTasks() {
        this.tasks.forEach((task) => {
          if (task.completed) {
            task.highlight = true;
          }
        });
        this.saveTasks();
      },
      filterImportantTasks() {
        this.tasks = this.tasks.filter((task) => task.important);
        this.saveTasks();
      },
      showAllTasks() {
        const savedTasks = localStorage.getItem("tasks");
        if (savedTasks) {
          this.tasks = JSON.parse(savedTasks);
        }
      },
      archiveCompletedTasks() {
        this.tasks = this.tasks.filter((task) => !task.completed);
        this.saveTasks();
      },
      setDueDate(index) {
        const newDate = prompt("Yeni bitiş tarihi girin (YYYY-MM-DD):");
        if (newDate) {
          this.tasks[index].dueDate = newDate;
          this.saveTasks();
        }
      },
      addRecurringTask() {
        if (this.newTask.trim() === "") return;
  
        const currentDate = new Date().toLocaleDateString("tr-TR");
        this.tasks.push({
          text: this.newTask,
          emoji: this.newEmoji,
          completed: false,
          important: false,
          selected: false,
          createdAt: currentDate,
          dueDate: null,
          dueDateMenu: false,
          recurring: true,
        });
        this.newTask = "";
        this.newEmoji = "";
        this.saveTasks();
      },
      addSubtask(index) {
        const subtaskText = prompt("Alt görev girin:");
        if (subtaskText) {
          if (!this.tasks[index].subtasks) {
            this.tasks[index].subtasks = [];
          }
          this.tasks[index].subtasks.push({ text: subtaskText, completed: false });
          this.saveTasks();
        }
      },
      showOverdueTasks() {
        const today = new Date();
        this.tasks.forEach((task) => {
          if (task.dueDate && new Date(task.dueDate) < today && !task.completed) {
            alert(`Gecikmiş Görev: ${task.text}`);
          }
        });
      },
      assignTaskToUser(index) {
        const user = prompt("Görevi atamak istediğiniz kullanıcı adı:");
        if (user) {
          this.tasks[index].assignedUser = user;
          this.saveTasks();
        }
      },
      pinTaskOrder() {
        this.tasks.sort((a, b) => b.important - a.important);
        this.saveTasks();
      },
      colorCodeTasks() {
        this.tasks.forEach((task) => {
          if (task.important) {
            task.color = "yellow";
          } else if (task.completed) {
            task.color = "green";
          } else {
            task.color = "white";
          }
        });
        this.saveTasks();
      },
      setTaskReminder() {
        const taskIndex = prompt("Hatırlatıcı ayarlamak istediğiniz görevin numarasını gir:");
        if (taskIndex && this.tasks[taskIndex]) {
          alert(`Hatırlatıcı ayarlandı: ${this.tasks[taskIndex].text}`);
        }
      },
      groupTasksByCategory() {
        const category = prompt("Kategori adını girin:");
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.category = category;
          }
        });
        this.saveTasks();
      },
      highlightImportantTasks() {
        this.tasks.forEach((task) => {
          if (task.important) {
            task.highlight = true;
          }
        });
        this.saveTasks();
      },
      sortByDueDate() {
        this.tasks.sort((a, b) => new Date(a.dueDate) - new Date(b.dueDate));
        this.saveTasks();
      },
      exportTasksToJSON() {
        const tasksJSON = JSON.stringify(this.tasks, null, 2);
        const blob = new Blob([tasksJSON], { type: "application/json" });
        const link = document.createElement("a");
        link.href = URL.createObjectURL(blob);
        link.download = "tasks.json";
        link.click();
      },
      importTasksFromJSON() {
        const input = document.createElement("input");
        input.type = "file";
        input.accept = "application/json";
        input.onchange = (event) => {
          const file = event.target.files[0];
          if (file) {
            const reader = new FileReader();
            reader.onload = (e) => {
              try {
                this.tasks = JSON.parse(e.target.result);
                this.saveTasks();
              } catch (error) {
                alert("Hatalı dosya formatı!");
              }
            };
            reader.readAsText(file);
          }
        };
        input.click();
      },
      duplicateTask() {
        const selectedTask = this.tasks.find((task) => task.selected);
        if (selectedTask) {
          const duplicatedTask = { ...selectedTask, createdAt: new Date().toLocaleDateString("tr-TR") };
          this.tasks.push(duplicatedTask);
          this.saveTasks();
        }
      },
      showTasksWithReminder() {
        const tasksWithReminder = this.tasks.filter(task => task.reminder);
        tasksWithReminder.forEach(task => {
          alert(`Hatırlatıcı Ayarlanmış Görev: ${task.text}`);
        });
      },
      markTasksAsUrgent() {
        this.tasks.forEach(task => {
          if (task.selected) {
            task.urgent = true;
          }
        });
        this.saveTasks();
      },
      addDeadline() {
        const selectedTask = this.tasks.find(task => task.selected);
        if (selectedTask) {
          const deadline = prompt("Son tarih girin (dd/mm/yyyy):");
          if (deadline) {
            selectedTask.deadline = deadline;
            this.saveTasks();
          }
        }
      },
      assignTasksToCategory() {
        const category = prompt("Belirli kategoriye atanacak görevleri seçin (örn: İş, Kişisel, Acil)");
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.category = category;
          }
        });
        this.saveTasks();
      },
      toggleTaskVisibility() {
        this.tasksVisible = !this.tasksVisible;
      },
      setPriorityLevels() {
        const priority = prompt("Görev öncelik seviyesini belirleyin (Yüksek, Orta, Düşük):");
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.priority = priority;
          }
        });
        this.saveTasks();
      },
      generateWeeklyReport() {
        let completedTasks = this.tasks.filter((task) => task.completed);
        let report = `Bu hafta tamamlanan görevler: \n`;
        completedTasks.forEach((task) => {
          report += `- ${task.text} (Tamamlanma Tarihi: ${task.completedAt || "Bilinmiyor"})\n`;
        });
        alert(report);
      },
      addCustomLabels() {
        const label = prompt("Özel etiket ekleyin (örn: Acil, Bugün, Bekleyen):");
        this.tasks.forEach((task) => {
          if (task.selected) {
            if (!task.labels) {
              task.labels = [];
            }
            task.labels.push(label);
          }
        });
        this.saveTasks();
      },
      assignMultipleTasks() {
        const assignee = prompt("Görev atamak istediğiniz kişinin adı:");
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.assignedTo = assignee;
          }
        });
        this.saveTasks();
      },
      trackTaskProgress() {
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.inProgress = !task.inProgress;
          }
        });
        this.saveTasks();
      },
      archiveOldTasks() {
        const today = new Date();
        this.tasks = this.tasks.filter((task) => {
          const taskDate = new Date(task.createdAt);
          return (today - taskDate) / (1000 * 60 * 60 * 24) < 30;
        });
        this.saveTasks();
      },
      shareTaskList() {
        alert("Görev listesi başarıyla paylaşıldı!");
      },
      copyTaskLink() {
        alert("Görev bağlantısı kopyalandı!");
      },
      setTaskColor() {
        const color = prompt("Görev için bir renk seçin (örn: kırmızı, mavi, yeşil):");
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.color = color;
          }
        });
        this.saveTasks();
      },
      sortByPriority() {
        this.tasks.sort((a, b) => {
          const priorityOrder = { "Yüksek": 3, "Orta": 2, "Düşük": 1 };
          return (priorityOrder[b.priority] || 0) - (priorityOrder[a.priority] || 0);
        });
        this.saveTasks();
      },
      markAsBlocked() {
        this.tasks.forEach((task) => {
          if (task.selected) {
            task.blocked = true;
          }
        });
        this.saveTasks();
      },
      duplicateSelectedTasks() {
        const selectedTasks = this.tasks.filter((task) => task.selected);
        selectedTasks.forEach((task) => {
          const duplicatedTask = { ...task, createdAt: new Date().toLocaleDateString("tr-TR") };
          this.tasks.push(duplicatedTask);
        });
        this.saveTasks();
      },
      linkTasks() {
        const taskLink = prompt("Birbirine bağlamak istediğiniz görevlerin numaralarını virgülle ayırarak girin:");
        const indices = taskLink.split(",").map((index) => parseInt(index.trim(), 10));
        indices.forEach((index) => {
          if (this.tasks[index]) {
            this.tasks[index].linked = true;
          }
        });
        this.saveTasks();
      },
      addCompletionTime() {
        this.tasks.forEach((task) => {
          if (task.completed && !task.completionTime) {
            task.completionTime = new Date().toLocaleTimeString("tr-TR");
          }
        });
        this.saveTasks();
      },
    },
  };
  </script>
  
  <style scoped>
  .done {
    text-decoration: line-through;
    color: gray;
  }
  .important {
    font-weight: bold;
    color: #ffa500;
  }
  .rounded-btn {
    border-radius: 12px;
  }
  .task-date {
    font-size: 0.8rem;
    color: #757575;
  }
  body {
    background-color: #121212;
    color: #ffffff;
    transition: background-color 0.5s, color 0.5s;
  }
  </style>
  