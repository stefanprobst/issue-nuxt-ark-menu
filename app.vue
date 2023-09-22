<script lang="ts" setup>
import "./global.css";

import { Menu, MenuTrigger, MenuPositioner, MenuContent, MenuItem } from "@ark-ui/vue/menu";

const menus = [
	{
		id: "one",
		label: "One",
		children: [
			{
				id: "one-one",
				label: "One One",
			},
			{
				id: "one-two",
				label: "One Two",
			},
		],
	},
	{
		id: "two",
		label: "Two",
		children: [
			{
				id: "two-one",
				label: "Two One",
			},
			{
				id: "two-two",
				label: "Two Two",
			},
		],
	},
];

const { data } = await useAsyncData(() => {
	return Promise.resolve(menus)
})
</script>

<template>
	<div class="min-h-full grid grid-rows-[auto_1fr_auto]">
		<header>
			<div class="w-full max-w-5xl mx-auto px-8 py-4 flex gap-8 justify-between items-center">
				<nav aria-label="Main" class="flex gap-2 items-center flex-wrap">
					<Menu v-for="menu of data">
						<MenuTrigger>
							<button class="font-medium px-4 py-2 rounded-md transition hover:bg-neutral-100">{{ menu.label }}</button>
						</MenuTrigger>
						<Teleport to="body">
							<MenuPositioner>
								<MenuContent class="shadow-lg bg-white rounded-md py-1.5">
									<MenuItem v-for="item of menu.children" :key="item.id" :id="item.id" class="flex w-full items-center py-2 px-3 hover:bg-neutral-100 transition rounded">
										{{ item.label }}
									</MenuItem>
								</MenuContent>
							</MenuPositioner>
						</Teleport>
					</Menu>
				</nav>
			</div>
		</header>

		<main>
			<h1>Hello, world!</h1>
		</main>

		<footer>
			<span>Footer</span>
		</footer>
	</div>
</template>
