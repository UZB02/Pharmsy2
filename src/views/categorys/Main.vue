<template>
  <!-- BEGIN: Modal Toggle -->
  <div class="text-center"></div>
  <!-- END: Modal Toggle -->
  <!-- BEGIN: ADD Modal Content -->
  <div id="basic-modal-preview" class="modal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <form
          @submit="addNewCategory($event)"
          class="bg-white shadow-md rounded flex gap-1 px-8 pt-6 pb-8 mb-4"
          typeof="submut"
        >
          <input
            v-model="InputValue"
            placeholder="New Category"
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            type="text"
          />
          <button class="btn btn-primary shadow-md mr-2" data-dismiss="modal">
            Add
          </button>
          <button
            type="button"
            data-dismiss="modal"
            id="close-modal"
            class="btn  btn-outline-secondary w-20 mr-1"
          >
            Cancel
          </button>
        </form>
        <!-- <LoadingIcon icon="bars" class="w-8 h-8" /> -->
      </div>
    </div>
  </div>
  <!-- END: Modal Content -->
  <!-- BEGIN: Edit Modal Content -->
  <div>
    <div
      id="static-backdrop-modal-preview"
      class="modal"
      data-backdrop="static"
      tabindex="-1"
    >
      <div class="modal-dialog">
        <div class="modal-body">
          <div class="bg-white  rounded flex gap-1 px-8 pt-6 pb-8 mb-4">
            <input
              type="text"
              v-model="editInputvalue"
              class="shadow-md  appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            />
            <button
              type="button"
              data-dismiss="modal"
              @click="editCategory(editInputvalue)"
              class="btn btn-primary w-24"
            >
              Edit
            </button>
            <button
              type="button"
              data-dismiss="modal"
              id="close-modal"
              class="btn  btn-outline-secondary w-20 mr-1"
            >
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- END: Modal Content -->
  <div>
    <h2 class="intro-y text-lg font-medium mt-10">Data List Layout</h2>
    <div class="grid grid-cols-12 gap-6 mt-5">
      <div
        class="intro-y col-span-12 flex flex-wrap sm:flex-nowrap items-center mt-2"
      >
        <a
          href="javascript:;"
          data-toggle="modal"
          data-target="#basic-modal-preview"
          class="btn btn-primary shadow-md mr-2"
          >Add New Category</a
        >

        <!-- <button  @click="addNewCategory">Add New Category</button> -->
        <div class="dropdown">
          <button
            class="dropdown-toggle btn px-2 box text-gray-700 dark:text-gray-300"
            aria-expanded="false"
          >
            <span class="w-5 h-5 flex items-center justify-center">
              <PlusIcon class="w-4 h-4" />
            </span>
          </button>
          <div class="dropdown-menu w-40">
            <div class="dropdown-menu__content box dark:bg-dark-1 p-2">
              <a
                href=""
                class="flex items-center block p-2 transition duration-300 ease-in-out bg-white dark:bg-dark-1 hover:bg-gray-200 dark:hover:bg-dark-2 rounded-md"
              >
                <PrinterIcon class="w-4 h-4 mr-2" /> Print
              </a>
              <a
                href=""
                class="flex items-center block p-2 transition duration-300 ease-in-out bg-white dark:bg-dark-1 hover:bg-gray-200 dark:hover:bg-dark-2 rounded-md"
              >
                <FileTextIcon class="w-4 h-4 mr-2" /> Export to Excel
              </a>
              <a
                href=""
                class="flex items-center block p-2 transition duration-300 ease-in-out bg-white dark:bg-dark-1 hover:bg-gray-200 dark:hover:bg-dark-2 rounded-md"
              >
                <FileTextIcon class="w-4 h-4 mr-2" /> Export to PDF
              </a>
            </div>
          </div>
        </div>
        <div class="hidden md:block mx-auto text-gray-600">
          <!-- Showing 1 to 10 of 150 entries -->
        </div>
        <div class="w-full sm:w-auto mt-3 sm:mt-0 sm:ml-auto md:ml-0">
          <div class="w-56 relative text-gray-700 dark:text-gray-300">
            <input
              type="text"
              v-model="searchKeyword"
              @input="searchData"
              class="form-control w-56 box pr-10 placeholder-theme-13"
              placeholder="Search..."
            />
            <SearchIcon
              class="w-4 h-4 absolute my-auto inset-y-0 mr-3 right-0"
            />
          </div>
        </div>
      </div>
      <!-- BEGIN: Data List -->
      <div class="intro-y col-span-12 overflow-auto lg:overflow-visible">
        <table class="table table-report -mt-2">
          <thead>
            <tr>
              <th
                class="whitespace-nowrap"
                style="display: flex;align-items: center; justify-content: center;transform: translate(-10px)"
              >
                Id
              </th>
              <th class="whitespace-nowrap">Nomi</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(faker, fakerKey) in data.value"
              :key="fakerKey"
              class="intro-x"
            >
              <td class="w-20">
                <div class="flex  justify-center">
                  <div
                    class="w-10 h-10 image-fi -ml-5"
                    style="display: flex; align-items: center;justify-content: center;"
                  >
                    {{ fakerKey + 1 }}
                  </div>
                </div>
              </td>
              <td>
                <a
                  href=""
                  class="font-medium whitespace-nowrap"
                  style="text-align: center;"
                  >{{ faker?.name }}</a
                >
              </td>
              <td class="table-report__action w-56">
                <div class="flex justify-center items-center">
                  <!-- <a href="javascript:;" data-toggle="modal"  class="btn btn-primary">Show Modal</a> -->

                  <a
                    href="javascript:;"
                    @click="modalEdit(faker)"
                    class="flex items-center mr-3"
                    data-toggle="modal"
                    data-target="#static-backdrop-modal-preview"
                  >
                    <Edit2Icon class="w-4 h-4 mr-1 fill-500 " />
                    Edit
                  </a>
                  <a
                    @click="modalDelete(faker.id)"
                    class="flex items-center text-theme-6"
                    href="javascript:;"
                    data-toggle="modal"
                    data-target="#delete-confirmation-modal"
                  >
                    <Trash2Icon class="w-4 h-4 mr-1" /> Delete
                  </a>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <!-- END: Data List -->
    </div>
    <!-- BEGIN: Delete Confirmation Modal -->
    <div v-if="modal">
      <div
        id="delete-confirmation-modal"
        class="modal"
        tabindex="-1"
        aria-hidden="true"
      >
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-body p-0">
              <div class="p-5 text-center">
                <XCircleIcon class="w-16 h-16 text-theme-6 mx-auto mt-3" />
                <div class="text-3xl mt-5">Are you sure?</div>
                <div class="text-gray-600 mt-2">
                  Do you really want to delete these records? <br />This process
                  cannot be undone.
                </div>
              </div>
              <div class="px-5 pb-8 text-center">
                <button
                  type="button"
                  id="cancelModal"
                  data-dismiss="modal"
                  class="btn btn-outline-secondary w-24 mr-1"
                >
                  Cancel
                </button>
                <button
                  type="button"
                  class="btn btn-danger w-24"
                  @click="deletCategory"
                >
                  Delete
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- END: Delete Confirmation Modal -->
  </div>
</template>

<script setup>
/* eslint-disable */
import { faker } from '@/utils/faker'
import axios from 'axios'
import { reactive, ref } from 'vue'
import Swal from 'sweetalert2'

const InputValue = ref('')
const editInputvalue = ref('')
const selectedId = ref(null)
const searchKeyword = ref('')
const data = reactive({})
const modal = ref(false)
const EditModalOpend = ref(false)
const eId = ref(null)

function modalDelete(id) {
  modal.value = true
  selectedId.value = id
}
function modalEdit(faker) {
  EditModalOpend.value = true
  editInputvalue.value = faker.name
  eId.value = faker.id
}

fetchData()

function fetchData() {
  axios
    .get('http://pharm-api.kdevs.uz/api/categories', {
      headers: {
        Authorization: 'Bearer ' + localStorage.getItem('token')
      }
    })
    .then(res => {
      data.value = res.data.result
    })
}
const addNewCategory = event => {
  event.preventDefault()
  axios
    .post(
      'http://pharm-api.kdevs.uz/api/categories',
      { name: InputValue.value },
      {
        headers: {
          Authorization: 'Bearer ' + localStorage.getItem('token')
        }
      }
    )
      .then(res => {
         Swal.fire({
          position: 'top-center',
          icon: 'success',
          title: 'Add successfully',
          showConfirmButton: false,
          timer: 1500
        })
      document.querySelector('#close-modal').click()
      fetchData()
    })
  InputValue.value = ''
}
const deletCategory = () => {
  axios
    .delete(`http://pharm-api.kdevs.uz/api/categories/${selectedId.value}`, {
      headers: {
        Authorization: 'Bearer ' + localStorage.getItem('token')
      }
    })
    .then(result => {
      // selectedId.value = result.id
        if (result.status === 200) {
         Swal.fire({
          position: 'top-center',
          icon: 'success',
          title: 'Delet successfully',
          showConfirmButton: false,
          timer: 1500
        })
        document.querySelector('#cancelModal').click()
        fetchData()
      }
    })

  // console.log(selectedId.value);
}

function searchData() {
  const token = localStorage.getItem('token')

  if (!searchKeyword.value) {
    fetchData()
    return
  }

  if (searchKeyword.value.length > 2) {
    axios
      .get('http://pharm-api.kdevs.uz/api/categories', {
        headers: {
          Authorization: 'Bearer ' + token
        },
        params: { search: searchKeyword.value }
      })
      .then(response => {
        data.value = response.data
      })
      .catch(error => {
        console.error(error)
      })
  }
}

const editCategory = e => {
  axios
    .put(
      `http://pharm-api.kdevs.uz/api/categories/${eId.value}`,
      {
        name: e
      },
      {
        headers: {
          Authorization: 'Bearer ' + localStorage.getItem('token')
        }
      }
    )
      .then(res => {
           Swal.fire({
          position: 'top-center',
          icon: 'success',
          title: 'Editted successfully',
          showConfirmButton: false,
          timer: 1500
           })
        console.log(e);
      fetchData()
      // document.querySelector('#close-modal').click()
    })
    .catch(error => {
      console.error(error)
    })
  //  document.querySelector('#close-modal').click()
}
</script>
