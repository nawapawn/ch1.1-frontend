<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">
      Version Control + Docker Demo (Quasar)
    </div>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Git Workflow (ตัวอย่างขั้นตอนทำงาน)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(step, index) in gitSteps" :key="index">
            <q-item-section avatar>
              <q-badge>{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ step.title }}</q-item-label>
              <q-item-label caption>{{ step.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Docker Concepts (สรุปสั้น ๆ)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerItems" :key="index">
            <q-item-section>
              <q-item-label>{{ item.title }}</q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- การ์ดการบ้าน: Docker Quick Reference -->
    <q-card>
      <q-card-section>
        <div class="text-h6">Docker Quick Reference (คำสั่งที่ใช้งานบ่อย)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(cmd, index) in dockerCommands" :key="index">
            <q-item-section avatar>
              <q-badge color="primary">{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label class="text-weight-bold text-primary">
                <code>{{ cmd.command }}</code>
              </q-item-label>
              <q-item-label caption>{{ cmd.description }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
const gitSteps = [
  {
    title: 'แก้โค้ด Quasar ใน src/',
    detail: 'เพิ่มหน้า / component ใหม่ เช่น IndexPage.vue, Layout ต่าง ๆ',
  },
  {
    title: 'ตรวจสอบสถานะไฟล์',
    detail: 'ใช้คำสั่ง `git status` ดูว่าไฟล์ไหนเปลี่ยนแปลงบ้าง',
  },
  {
    title: 'เพิ่มไฟล์เข้า staging',
    detail: 'จากรากโปรเจกต์ ใช้ git add frontend/src/pages/IndexPage.vue',
  },
  {
    title: 'สร้าง commit พร้อมข้อความแบบ Conventional Commits',
    detail: 'เช่น `feat: add Git workflow demo page`',
  },
  {
    title: 'push ขึ้น GitHub',
    detail: 'ใช้ git push -u origin feature/quasar-demo แล้วเปิด Pull Request',
  },
]

const dockerItems = [
  {
    title: 'Image',
    detail: 'แพ็กเกจที่มีไฟล์และการตั้งค่าที่ใช้สร้าง container เช่น image ที่รวม Quasar SPA กับ Nginx',
  },
  {
    title: 'Container',
    detail: 'อินสแตนซ์ที่สร้างจาก image เช่น container ที่รัน Nginx เพื่อเสิร์ฟไฟล์ Quasar',
  },
  {
    title: 'Volume',
    detail: 'เก็บข้อมูลให้คงอยู่แยกจากวงจรชีวิตของ container เช่น ไฟล์อัปโหลดของ backend',
  },
  {
    title: 'Network',
    detail: 'ให้บริการใน Docker ติดต่อกันได้ เช่น Nginx ส่งต่อคำขอไปยัง Express',
  },
]

const dockerCommands = [
  {
    command: 'docker build -t <image-name> -f frontend/Dockerfile ./frontend',
    description: 'ใช้สร้าง Docker Image ใหม่จากไฟล์ Dockerfile เมื่อมีการแก้ไขโค้ดหรือการตั้งค่าแอปพลิเคชัน',
  },
  {
    command: 'docker run -d -p 8080:80 --name <container-name> <image-name>',
    description: 'ใช้สร้างและสั่งรัน Container แบบทำงานเบื้องหลัง (-d) พร้อมเชื่อมพอร์ต 8080 ของเครื่องเข้ากับพอร์ต 80 ของ Container',
  },
  {
    command: 'docker ps',
    description: 'ใช้ตรวจสอบรายชื่อ สถานะการทำงาน และพอร์ตของ Container ที่กำลังเปิดทำงานอยู่ในปัจจุบัน',
  },
  {
    command: 'docker compose up -d --build',
    description: 'ใช้สั่ง build image ใหม่และเริ่มต้นการทำงานของบริการทั้งหมดที่กำหนดไว้ในไฟล์ docker-compose.yml พร้อมกัน',
  },
  {
    command: 'docker compose down',
    description: 'ใช้หยุดการทำงานและลบ Container รวมถึง Network ที่ถูกสร้างขึ้นจาก Docker Compose เพื่อคืนทรัพยากรและพอร์ตระบบ',
  },
]
</script>