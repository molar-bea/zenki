<template>
  <div class="about-us">
    <h2>Our Team</h2>
    <div class="team-grid">
      <div v-for="member in teamMembers" :key="member.id" class="team-card">
        <router-link :to="`/team/${member.id}`" class="member-link">
          <h3>{{ member.name }}</h3>
        </router-link>
        <p class="role">{{ member.role }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AboutUs',
  data() {
    return {
      teamMembers: [
        { id: 1, name: 'Bea R. Molar', role: 'Project Manager' },
        { id: 2, name: 'Gian Carlo J. Suico', role: 'Database Designer' },
        { id: 3, name: 'Nexus F. Paloma', role: 'Web Designer' },
        { id: 3, name: 'Raniel John B. Flores', role: 'Web Designer' },
        { id: 3, name: 'Exzon Y. Mendoza II', role: 'Web Designer' },
        { id: 6, name: 'Jo Mari Jess Y. Cormanes', role: 'Backend Developer' }
      ]
    }
  }
}
</script>

<style scoped>
.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5rem;
}

.team-card {
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  text-align: center;
  transition: transform 0.2s;
}

.team-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.member-link {
  text-decoration: none;
  color: #2c3e50;
  transition: color 0.2s;
}

.member-link:hover h3 {
  color: #42b983;
}

.role {
  color: #666;
  font-style: italic;
  margin-top: 0.5rem;
}
</style>