<template>
	<li>
		<!-- If item.href is set, a link will be directly used -->
		<a v-if="item.href" :href="item.href">
			<span :class="item.icon"></span>
			<span v-if="item.text">{{item.text}}</span>
			<p v-else-if="item.longtext">{{item.longtext}}</p>
		</a>
		<!-- If item.action is set instead, a button will be used -->
		<button @click="item.action" v-else-if="item.action">
			<span :class="item.icon"></span>
			<span v-if="item.text">{{item.text}}</span>
			<p v-else-if="item.longtext">{{item.longtext}}</p>
		</button>
		<!-- If item.longtext is set AND the item does not have an action -->
		<span v-else class="menuitem">
			<span :class="item.icon"></span>
			<span v-if="item.text">{{item.text}}</span>
			<p v-else-if="item.longtext">{{item.longtext}}</p>
		</span>
	</li>
</template>

<script>
export default {
	props: ['item']
};
</script>

<style lang="scss" scoped>
$popoveritem-height: 38px;
$popovericon-size: 16px;


li {
	display: flex;
	flex: 0 0 auto;
	> button,
	> a,
	> .menuitem {
		cursor: pointer;
		line-height: $popoveritem-height;
		border: 0;
		background-color: transparent;
		display: flex;
		align-items: flex-start;
		height: auto;
		margin: 0;
		font-weight: 300;
		box-shadow: none;
		width: 100%;
		color: $color-main-text;
		/* Override the app-navigation li opacity */
		opacity: 0.7 !important;
		span[class^='icon-'],
		span[class*=' icon-'],
		&[class^='icon-'],
		&[class*=' icon-'] {
			min-width: 0; /* Overwrite icons*/
			min-height: 0;
			background-position: #{($popoveritem-height - $popovericon-size) / 2} center;
			background-size: $popovericon-size;
		}
		span[class^='icon-'],
		span[class*=' icon-'] {
			/* Keep padding to define the width to
				assure correct position of a possible text */
			padding: #{$popoveritem-height / 2} 0 #{$popoveritem-height / 2} $popoveritem-height;
		}
		// If no icons set, force left margin to align
		&:not([class^='icon-']):not([class*='icon-']) {
			> span,
			> input,
			> form {
				&:not([class^='icon-']):not([class*='icon-']):first-child {
					margin-left: $popoveritem-height;
				}
			}
		}
		&[class^='icon-'],
		&[class*=' icon-'] {
			padding: 0 #{($popoveritem-height - $popovericon-size) / 2} 0 $popoveritem-height !important;
		}
		&:hover,
		&:focus,
		&.active {
			opacity: 1 !important;
		}
		/* prevent .action class to break the design */
		&.action {
			padding: inherit !important;
		}
		> span {
			cursor: pointer;
			white-space: nowrap;
		}
		> p {
			width: 150px;
			line-height: 1.6em;
			padding: 8px 0;
		}
		> select {
			margin: 0;
			margin-left: 6px;
		}
		/* Add padding if contains icon+text */
		&:not(:empty) {
			padding-right: 10px !important;
		}
		/* DEPRECATED! old img in popover fallback
		 * TODO: to remove */
		> img {
			width: $popovericon-size;
			padding: #{($popoveritem-height - $popovericon-size) / 2};
		}
		/* checkbox/radio fixes */
		> input.radio + label,
		> input.checkbox + label {
			padding: 0 !important;
			width: 100%;
		}
		> input.checkbox + label::before {
			margin: -2px 13px 0;
		}
		> input.radio + label::before {
			margin: -2px 12px 0;
		}
		> input:not([type='radio']):not([type='checkbox']):not([type='image']) {
			width: 150px;
		}
		form {
			display: flex;
			flex: 1 1 auto;
			/* put a small space between text and form
				if there is an element before */
			&:not(:first-child) {
				margin-left: 5px;
			}
		}
		/* no margin if hidden span before */
		> span.hidden + form,
		> span[style*='display:none'] + form {
			margin-left: 0;
		}
		/* Inputs inside popover supports text, submit & reset */
		input {
			min-width: #{$popoveritem-height - 4px}; /* twice the margin */
			max-height: #{$popoveritem-height - 4px}; /* twice the margin */
			margin: 2px 0;
			flex: 1 1 auto;
			&:not(:first-child) {
				margin-left: 5px;
			}
		}
	}
	/* css hack, only first not hidden*/
	&:not(.hidden):not([style*='display:none']) {
		&:first-of-type {
			> button,
			> a,
			> .menuitem {
				> form,
				> input {
					margin-top: 10px;
				}
			}
		}
		&:last-of-type {
			> button,
			> a,
			> .menuitem {
				> form,
				> input {
					margin-bottom: 10px;
				}
			}
		}
	}
	> button {
		padding: 0;
		span {
			opacity: 1;
		}
	}
}
</style>
