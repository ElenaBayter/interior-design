<template>
  <div>
    <!-- -->
  </div>
</template>

<script>
export default {
  name: 'PaginationTest',

  methods: {
  updateFilteredProjects() {
    // Фильтрация проектов по выбранным тегам
    const filtered = this.progects.filter(project =>
      project.tags.some(tag => this.selectedTags.includes(tag))
    );

    // Вычисление общего количества страниц
    const totalPages = Math.ceil(filtered.length / this.itemsPerPage);
    this.totalPages = totalPages; 

    // Вычисление индексов для текущей страницы
    const pageNumber = this.getCurrentPageNumber();
    const startIndex = (pageNumber - 1) * this.itemsPerPage;
    const endIndex = startIndex + this.itemsPerPage;

    // Получение проектов для текущей страницы
    const paginatedProjects = filtered.slice(startIndex, endIndex);
    this.paginatedProjects = paginatedProjects; // Убедитесь, что paginatedProjects теперь в data
  }
},
watch: {
  selectedTags: {
    handler() {
      this.updateFilteredProjects();
    },
    immediate: true,
    deep: true
  },
  '$route.params.pageNumber': {
    handler() {
      this.updateFilteredProjects();
    },
    immediate: true
  }
},
data() {
  return {
    // Ваши существующие данные
    totalPages: 0, // Для хранения общего количества страниц
    paginatedProjects: [] // Для хранения проектов текущей страницы
  };
},
};
</script>