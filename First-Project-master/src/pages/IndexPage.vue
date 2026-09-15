<template>
  <div class="q-pa-md">

    <!-- 1. ส่วนกรอกข้อมูลของคุณ (แก้เรื่องสีชนกันให้แล้ว) -->
    <div class="q-gutter-y-md column" style="max-width: 400px">
      <q-input color="purple-12" v-model="text" label="พิมพ์คอมเมนต์ของคุณที่นี่...">
        <template v-slot:prepend>
          <q-icon name="event" />
        </template>
      </q-input>

      <!-- ปุ่มกดเพื่อเพิ่มคอมเมนต์ -->
      <q-btn color="primary" label="โพสต์คอมเมนต์" icon="send" @click="addComment" />
    </div>

    <q-separator class="q-my-lg" />

    <!-- 2. ส่วนแสดงรายการคอมเมนต์ และ "ปุ่มลบ (Delete)" ที่อาจารย์ต้องการ -->
    <div style="max-width: 400px">
      <h6 class="q-mb-md">รายการความคิดเห็น</h6>

      <q-list bordered separator>
        <!-- วนลูปแสดงคอมเมนต์ -->
        <q-item v-for="(comment, index) in comments" :key="index">
          <q-item-section>
            <q-item-label>{{ comment }}</q-item-label>
          </q-item-section>

          <!-- 🔥 ตรงนี้แหละคือ "Comment Delete" ที่อาจารย์หาอยู่ 🔥 -->
          <q-item-section side>
            <q-btn
              flat
              round
              color="negative"
              icon="delete"
              @click="deleteComment(index)"
            >
              <q-tooltip>ลบคอมเมนต์</q-tooltip>
            </q-btn>
          </q-item-section>
        </q-item>

        <!-- แสดงข้อความนี้ถ้ายังไม่มีใครคอมเมนต์ -->
        <q-item v-if="comments.length === 0">
          <q-item-section class="text-grey text-center">
            ยังไม่มีคอมเมนต์
          </q-item-section>
        </q-item>
      </q-list>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

// ตัวแปรเก็บข้อความในช่อง Input
const text = ref('')

// ตัวแปรเก็บรายการคอมเมนต์ทั้งหมด (เป็น Array)
const comments = ref([])

// ฟังก์ชันเพิ่มคอมเมนต์
const addComment = () => {
  if (text.value.trim() !== '') {
    comments.value.push(text.value) // เอาข้อความยัดใส่ Array
    text.value = '' // ล้างช่อง Input ให้ว่างหลังจากโพสต์เสร็จ
  }
}

// 🔥 ฟังก์ชันสำหรับ "ลบคอมเมนต์" (Comment Delete) 🔥
const deleteComment = (index) => {
  comments.value.splice(index, 1) // ลบข้อมูลออกจาก Array ตามตำแหน่งที่กด
}
</script>
