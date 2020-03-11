<template>
  <div class="bg-white px-4 py-3 flex items-center justify-between sm:px-6">
<!--
    <div class="flex-1 flex justify-between hidden">
      <a href="#" class="relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm leading-5 font-medium rounded-md text-gray-700 bg-white hover:text-gray-500 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150">
        Previous
      </a>
      <a href="#" class="ml-3 relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm leading-5 font-medium rounded-md text-gray-700 bg-white hover:text-gray-500 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150">
        Next
      </a>
    </div>
 -->
 <!-- <ul>
    <li v-for="todo in todos"
    :key="todo.id">
      <a href="#" class="block hover:bg-gray-50 focus:outline-none focus:bg-gray-50 transition duration-150 ease-in-out">
        <div class="flex items-center px-4 py-4 sm:px-6">
          <div class="min-w-0 flex-1 flex items-center">
            <div class="flex-shrink-0">
              <img class="h-12 w-12 rounded-full" src="https://picsum.photos/200/300" alt="" />
            </div>
            <div class="min-w-0 flex-1 px-4 md:grid md:grid-cols-2 md:gap-4">
              <div>
                <div class="text-sm leading-5 font-medium text-indigo-600 truncate">{{ todo.to_location }} {{ todo.destination_city }} </div>
                <div class="mt-2 flex items-center text-sm leading-5 text-gray-500">
                  <svg class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884zM18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" clip-rule="evenodd"/>
                  </svg>
                  <span class="truncate"> Price: $ {{ todo.local_price }}</span>
                </div>
              </div>
              <div class="hidden md:block">
                <div>
                  <div class="text-sm leading-5 text-gray-900">
                    Departure Date
                    <time datetime="2020-01-07"> {{ todo.outbound_departure_dt }} </time>
                  </div>
                  <div class="mt-2 flex items-center text-sm leading-5 text-gray-500">
                    <svg class="flex-shrink-0 mr-1.5 h-5 w-5 text-green-400" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                    </svg>
                    Completed phone screening
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div>
            <svg class="h-5 w-5 text-gray-400" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"/>
            </svg>
          </div>
        </div>
      </a>
    </li>
  </ul> -->
    <div class="hidden sm:flex-1 sm:flex sm:items-center sm:justify-between">
      <div>
        <p class="text-sm leading-5 text-gray-700">
          Showing
          <span class="font-medium">{{ firstItem + 1 }}</span>
          to
          <span class="font-medium">{{ lastItem }}</span>
          of
          <span class="font-medium">{{ totalItems }}</span>
          results
        </p>
      </div>
      <div>
        <span class="relative z-0 inline-flex shadow-sm">
          <button @click="firstPage" :disabled="prevDisabled" type="button" class="hidden sm:inline-flex relative items-center px-2 py-2 rounded-l-md border border-gray-300 bg-white text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150" :class="{ 'text-gray-500 hover:text-gray-400': !prevDisabled, 'text-gray-400': prevDisabled }">
            <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M13.707 5.293a1 1 0 010 1.414L10.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd"/>
              <path fill-rule="evenodd" d="M7 5a1 1 0 011 1v8a1 1 0 11-2 0V6a1 1 0 011-1z" clip-rule="evenodd"/>
            </svg>
          </button>
          <button @click="prevPage" :disabled="prevDisabled" type="button" class="sm:-ml-px relative inline-flex items-center px-2 py-2 rounded-l-md sm:rounded-none border border-gray-300 bg-white text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150" :class="{ 'text-gray-500 hover:text-gray-400': !prevDisabled, 'text-gray-400': prevDisabled }">
            <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd"/>
            </svg>
          </button>

          <!-- // eslint-disable-next-line vue/require-v-for-key -->
          <span v-for="page in pages"
          :key="page">
            <button @click="gotoPage(page - 1)" type="button"
              class="-ml-px relative hidden md:inline-flex items-center px-4 py-2 border border-gray-300 text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-indigo-300 focus:shadow-outline-indigo active:bg-indigo-200 active:text-gray-700 transition ease-in-out duration-150 hover:bg-indigo-50"
              :class="{ 'bg-indigo-100 text-indigo-700': tinted && page === currentPage + 1, 'bg-white text-gray-700': page !== currentPage + 1 }">
              {{ page }}
            </button>
          </span>

          <button @click="nextPage" :disabled="nextDisabled" type="button" class="-ml-px relative inline-flex items-center px-2 py-2 rounded-r-md sm:rounded-none border border-gray-300 bg-white text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150" :class="{ 'text-gray-500 hover:text-gray-400': !nextDisabled, 'text-gray-400': nextDisabled }">
            <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"/>
            </svg>
          </button>
          <button @click="lastPage" :disabled="nextDisabled" type="button" class="-ml-px relative hidden sm:inline-flex items-center px-2 py-2 rounded-r-md border border-gray-300 bg-white text-sm leading-5 font-medium focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150" :class="{ 'text-gray-500 hover:text-gray-400': !nextDisabled, 'text-gray-400': nextDisabled }">
            <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M6.293 5.293a1 1 0 000 1.414L9.586 10l-3.293 3.293a1 1 0 001.414 1.414l4-4a1 1 0 000-1.414l-4-4a1 1 0 00-1.414 0z" clip-rule="evenodd"/>
              <path fill-rule="evenodd" d="M13 5a1 1 0 00-1 1v8a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
            </svg>
          </button>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
// pagination logic adapted from https://github.com/cornflourblue/jw-paginate

export default {
  props: {
    totalItems: {
      type: Number,
      required: true
    },
    itemsPerPage: {
      type: Number,
      required: false,
      default: 15
    },
    maxPages: {
      type: Number,
      required: false,
      default: 5
    },
    tinted: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data () {
    return {
      currentPage: 0
    }
  },
  computed: {
    nextDisabled () {
      return this.currentPage >= this.totalPages - 1
    },
    prevDisabled () {
      return this.currentPage === 0
    },
    lastItem () {
      return this.firstItem + this.itemsPerPage <= this.totalItems
        ? this.firstItem + this.itemsPerPage
        : this.totalItems
    },
    firstItem () {
      return this.currentPage * this.itemsPerPage
    },
    totalPages () {
      return Math.ceil(this.totalItems / this.itemsPerPage)
    },
    minPage () {
      return Math.floor(this.maxPages / 2)
    },
    maxPage () {
      return Math.ceil(this.maxPages / 2) - 1
    },
    startPage () {
      if (this.totalPages <= this.maxPages || this.currentPage <= this.minPage) { return 1 } else if (this.currentPage + this.maxPage >= this.totalPages) { return this.totalPages - this.maxPages + 1 }

      return this.currentPage - this.minPage + 1
    },
    endPage () {
      if (this.totalPages <= this.maxPages || this.currentPage + this.maxPage >= this.totalPages) { return this.totalPages } else if (this.currentPage <= this.minPage) { return this.maxPages }

      return this.currentPage + this.maxPage + 1
    },
    pages () {
      return Array.from(Array((this.endPage + 1) - this.startPage).keys()).map(i => this.startPage + i)
    }
  },
  methods: {
    isPage (page) {
      return page <= 3 || page >= this.totalPages - 2
    },
    nextPage () {
      if (this.currentPage < this.totalPages - 1) { this.currentPage++ }
      this.$emit('next-page')
    },
    prevPage () {
      if (this.currentPage > 0) { this.currentPage-- }
      this.$emit('prev-page')
    },
    firstPage () {
      this.currentPage = 0
      this.$emit('goto-index', this.currentPage)
    },
    lastPage () {
      this.currentPage = this.totalPages - 1
      this.$emit('goto-index', this.currentPage)
    },
    gotoPage (page) {
      this.currentPage = page
      this.$emit('goto-index', this.currentPage)
    }
  }
}
</script>
