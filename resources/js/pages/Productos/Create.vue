<template>
    <div class="container mx-auto px-4 py-8">
      <div class="max-w-2xl mx-auto">
        <h1 class="text-2xl font-bold mb-6">Crear Nuevo Producto</h1>
  
        <form @submit.prevent="submit" class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="nombre">
              Nombre
            </label>
            <input
              v-model="form.nombre"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="nombre"
              type="text"
              required
            />
          </div>
  
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="identificador">
              Identificador
            </label>
            <input
              v-model="form.identificador"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="identificador"
              type="text"
              required
            />
          </div>
  
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="descripcion">
              Descripción
            </label>
            <textarea
              v-model="form.descripcion"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="descripcion"
              rows="3"
            ></textarea>
          </div>
  
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="precio">
              Precio
            </label>
            <input
              v-model="form.precio"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="precio"
              type="number"
              step="0.01"
              min="0"
              required
            />
          </div>
  
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="stock">
              Stock
            </label>
            <input
              v-model="form.stock"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="stock"
              type="number"
              min="0"
              required
            />
          </div>
  
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="categoria_id">
              Categoría
            </label>
            <select
              v-model="form.categoria_id"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="categoria_id"
              required
            >
              <option value="">Seleccione una categoría</option>
              <option v-for="categoria in categorias" :key="categoria.id" :value="categoria.id">
                {{ categoria.nombre }}
              </option>
            </select>
          </div>
  
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="estado">
              Estado
            </label>
            <select
              v-model="form.estado"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="estado"
              required
            >
              <option :value="true">Activo</option>
              <option :value="false">Inactivo</option>
            </select>
          </div>
  
          <div class="flex items-center justify-between">
            <Link
              :href="route('productos.index')"
              class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            >
              Cancelar
            </Link>
            <button
              type="submit"
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              :disabled="form.processing"
            >
              Guardar
            </button>
          </div>
        </form>
      </div>
    </div>
  </template>
  
  <script setup>
  import { Link, useForm } from '@inertiajs/vue3';
  import AppLayout from '@/layouts/AppLayout.vue';
  
  const props = defineProps({
    categorias: Array
  });
  
  const form = useForm({
    nombre: '',
    identificador: '',
    descripcion: '',
    precio: '',
    stock: '',
    categoria_id: '',
    estado: true
  });
  
  const submit = () => {
    form.post(route('productos.store'));
  };
  </script>
  
  <script>
  export default {
    layout: AppLayout
  }
  </script>
  