<template>
	<div class="popovermenu open">
		<ul>
			<popover-item v-for="(item, key) in menu" :item="item" :key="key" />
		</ul>
	</div>
</template>


<script>
import popoverItem from './popoverItem';

export default {
	name: 'popoverMenu',
	props: {
		menu: {
			type: Array,
			default: () => [
				{
					icon: 'icon-delete',
					text: 'Delete item',
					action: () => {
						alert('Deleted!');
					}
				},
				{
					icon: 'icon-nextcloud',
					text: 'Nextcloud website',
					href: 'https://nextcloud.com'
				},
				{
					icon: 'icon-details',
					longtext: 'Add item'
				}
			]
		}
	},
	components: {
		popoverItem
	}
};
</script>

<style lang="scss" scoped>
.popovermenu {
	position: absolute;
	background-color: $color-main-background;
	color: $color-main-text;
	border-radius: $border-radius;
	z-index: 110;
	margin: 5px;
	margin-top: -5px;
	right: 0;
	filter: drop-shadow(0 1px 3px $color-box-shadow);
	display: none;

	&:after {
		bottom: 100%;
		/* Min-width of popover is 36px and arrow width is 20px
		wich leaves us 8px right and 8px left */
		right: 8px;
		/* change this to adjust the arrow position */
		border: solid transparent;
		content: ' ';
		height: 0;
		width: 0;
		position: absolute;
		pointer-events: none;
		border-bottom-color: $color-main-background;
		border-width: 10px;
	}
	/* Center the popover */
	&.menu-center {
		transform: translateX(50%);
		right: 50%;
		margin-right: 0;
		&:after {
			right: 50%;
			transform: translateX(50%);
		}
	}
	/* Align the popover to the left */
	&.menu-left {
		right: auto;
		left: 0;
		margin-right: 0;
		&:after {
			left: 6px;
			right: auto;
		}
	}

	&.open {
		display: block;
	}

	ul {
		/* Overwrite #app-navigation > ul ul */
		display: flex !important;
		flex-direction: column;
	}
}
</style>

