<!--
  - @copyright Copyright (c) 2018 John Molakvoæ <skjnldsv@protonmail.com>
  -
  - @author John Molakvoæ <skjnldsv@protonmail.com>
  -
  - @license GNU AGPL version 3 or any later version
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as
  - published by the Free Software Foundation, either version 3 of the
  - License, or (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program. If not, see <http://www.gnu.org/licenses/>.
  -
  -->

<template>
	<div id="app-navigation" :class="{'icon-loading': menu.loading}">
		<div v-if="menu.new" class="app-navigation-new">
			<button :id="menu.new.id" :class="menu.new.icon" type="button"
				:disabled="menu.new.disabled" @click="menu.new.action">
				{{ menu.new.text }}
			</button>
		</div>
		<ul :id="menu.id">
			<app-navigation-item v-for="item in menu.items" :key="item.key" :item="item" />
		</ul>
		<div v-if="!!$slots['settings-content']" id="app-settings" v-click-outside="closeMenu"
			:class="{open: opened}">
			<div id="app-settings-header">
				<button class="settings-button"
					data-apps-slide-toggle="#app-settings-content"
					@click="toggleMenu">
					{{ t('contacts', 'Settings') }}
				</button>
			</div>
			<div id="app-settings-content">
				<slot name="settings-content" />
			</div>
		</div>
	</div>
</template>

<script>
import AppNavigationItem from './AppNavigationItem'
import ClickOutside from 'vue-click-outside'

export default {
	name: 'AppNavigation',
	components: {
		AppNavigationItem
	},
	directives: {
		ClickOutside
	},
	props: {
		menu: {
			type: Object,
			required: true,
			default: () => {
				return {
					new: {
						id: 'new-item',
						action: () => alert('Success!'),
						icon: 'icon-add',
						text: 'New item'
					},
					items: []
				}
			}
		}
	},
	data() {
		return {
			opened: false
		}
	},
	methods: {
		toggleMenu() {
			this.opened = !this.opened
		},
		closeMenu() {
			this.opened = false
		}
	}
}
</script>
