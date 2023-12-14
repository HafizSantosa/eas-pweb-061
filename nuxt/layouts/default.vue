<template>
    <nav class="flex justify-around bg-gray-200 p-4 shadow-md">
        <div>
            <NuxtLink to="/submission">
                <button type="button" class="text-white bg-blue-500 hover:bg-blue-700 font-bold py-2 px-4 rounded">Create</button>
            </NuxtLink>
        </div>
        <div>
            <NuxtLink to="/cards">
                <button type="button" class="text-white bg-blue-500 hover:bg-blue-700 font-bold py-2 px-4 rounded">Check</button>
            </NuxtLink>
        </div>
        <div>
            <NuxtLink to="/emailcheck">
                <button type="button" class="text-white bg-green-500 hover:bg-green-700 font-bold py-2 px-4 rounded">Status</button>
            </NuxtLink>
        </div>
    </nav>
</template>
