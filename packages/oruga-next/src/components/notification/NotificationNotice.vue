<template>
    <o-notification
        v-bind="propsNotification"
        @close="close">
        <slot />
    </o-notification>
</template>

<script>
import { getOptions } from '../../utils/config'
import { getValueByPath } from '../../utils/helpers'
import NoticeMixin from '../../utils/NoticeMixin'
import BaseComponentMixin from '../../utils/BaseComponentMixin'

/**
 * @displayName Notification Notice
 */
export default {
    name: 'ONotificationNotice',
    configField: 'notice',
    mixins: [BaseComponentMixin, NoticeMixin],
    emits: ['update:active', 'close'],
    props: {
        propsNotification: Object,
    },
    data() {
        return {
            newDuration: this.duration || getValueByPath(getOptions(), 'notification.duration', 1000)
        }
    },
    methods: {
        rootClasses() {
            return [
                this.computedClass('rootClass', 'o-notices'),
            ]
        },
        positionClasses(position) {
            return [
                this.computedClass('positionClass', 'o-notices--', position),
            ]
        },
    }
}
</script>
