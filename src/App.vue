<template>
  <!-- <img :src="logoURL" :alt="logoCaption" width="200" height="200" /> -->

  <h1 style="margin-bottom: 16px">{{ title }}</h1><hr>

  <div>
    <p align="right">
      วันที่ <input type="date" name="" id="" required v-model="newDate" />
    </p>

    <div class="row" style="margin-bottom: 10px">
      <div class="col">
        <text>ชื่อ</text>
        <input
          type="text"
          class="form-control"
          placeholder="ชื่อ"
          aria-label="ชื่อ"
          v-model="newFname"
        />
      </div>
      <div class="col">
        <text>นามสกุล</text>
        <input
          type="text"
          class="form-control"
          placeholder="นามสกุล"
          aria-label="นามสกุล"
          v-model="newLname"
        />
      </div>
    </div>

    <div style="margin-bottom: 10px">
      <text>คณะที่เรียน</text>
      <select class="form-select"  aria-label="คณะที่เรียน" v-model="newGroup">
        <option selected>เลือกคณะที่เรียน</option>
        <option value="คณะวิทยาศาสตร์">คณะวิทยาศาสตร์</option>
        <option value="คณะบริหารธุรกิจ">คณะบริหารธุรกิจ</option>
        <option value="อื่นๆ">...</option>
      </select>
    </div>

    <div style="margin-bottom: 10px">
      <text>สาขาที่เรียน</text>
      <input
        class="form-control"
        type="text"
        placeholder="สาขา"
        aria-label="สาขา"
        v-model="newBranch"
      />
    </div>

    <div style="margin-bottom: 10px">
      <text>รหัสนักศึกษา</text>
      <input
        class="form-control"
        type="number"
        placeholder="รหัสนักศึกษา"
        aria-label="รหัสนักศึกษา"
        v-model="newCode"
        @keyup.enter="addTask"
      />
    </div>

    <button @click="addTask" :disabled="newCode.length < 1" style="margin-bottom: 5px">เช็คชื่อ</button>
    <br>
    <hr>
    <span
      >รายชื่อคนเช็คชื่อ {{ allTask }} {{ allTask > 1 ? "คน" : "คน" }}
    </span>
    <br />

    <ul>
      <li
        v-for="(task) in latest"
        :key="task.id"
        @click="finishTask(task)"
        :class="{ strikeout: task.finished }"
      >
        {{ task.date }} | {{ task.fname }} {{ task.lname }} | {{ task.group }} 
        <br>| {{ task.branch }} | รหัสนักศึกษา : {{ task.code }}  

        <div v-if="task.finished">
          <button @click="removeTask(task.id)">คลิกเพื่อลบรายชื่อ</button>
        </div>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "เช็คชื่อเข้าอบรม",
      newFname: "",
      newLname: "",
      newCode: "",
      newGroup: "",
      newBranch: "",
      newDate: "",
      logoURL: "https://unsplash.com/photos/0J8thHZfosE",
      logoCaption: "this is caption",
      tasks: [
        {
          id: 1,
          fname: "สุรพล",
          lname: "บุญดี",
          code: "1111111111",
          group: "คณะวิทยาศาสตร์",
          branch: "สาขาวิทยาการคอมพิวเตอร์",
          date: "2023-01-20",
          finished: true,
        },
        {
          id: 2,
          fname: "เรวิทย์",
          lname: "จันทรเกียรติ",
          code: "2222222222",
          group: "คณะวิทยาศาสตร์",
          branch: "สาขาวิทยาการคอมพิวเตอร์",
          date: "2023-01-22",
          finished: false,
        },
        {
          id: 3,
          fname: "ยศกร",
          lname: "ธาราวงศ์",
          code: "3333333333",
          group: "คณะวิทยาศาสตร์",
          branch: "สาขาวิทยาการคอมพิวเตอร์",
          date: "2023-01-26",
          finished: false,
        },
      ],
    };
  },
  methods: {
    addTask() {
      if (this.newCode.length < 1) return;

      this.tasks.push({
        id: this.tasks.length + 1,
        fname: this.newFname,
        lname: this.newLname,
        code: this.newCode,
        group: this.newGroup,
        branch: this.newBranch,
        date: this.newDate,
        finished: false,
      });

      this.newCode = "";
    },
    finishTask(task) {
      task.finished = !task.finished;
    },
    removeTask(taskID) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== taskID;
      });
    },
  },
  computed: {
    allTask() {
      return this.tasks.length;
    },
    latest() {
      return [...this.tasks].reverse();
    },
  },
};
</script>

<style>
.strikeout {
  text-decoration: line-through;
}
</style>
