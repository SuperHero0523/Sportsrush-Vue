<template>
    <div class="LeftMenu" is="sui-container">
        <sui-menu >
            <sui-menu-item class="LeftItemB" icon="handshake outline big" @click.native="activeItem('teams')" :class="{'active' : teamsActive}" >My Teams</sui-menu-item>
            <sui-menu-item class="LeftItemB" icon="alarm big" @click.native="activeItem('notif')" :class="{'active' : notifActive}" ><span class="badge red">{{ getInvitationsCount + getUnseenPMsCount + getUnseenMessagesCount }}</span></sui-menu-item>
        </sui-menu>
    </div>
</template>

<script>
    import { mapGetters } from 'vuex'
            export default {
                data() {
                    return {
                        teamsActive: true,
                        notifActive: false,
                        getInvitationsCount: 0,
                        getUnseenPMsCount: 0,
                        getUnseenMessagesCount: 0
                    }
                },
                methods: {
                    activeItem(item, event) {
                        if (item == 'teams') {
                            this.teamsActive = true;
                            this.notifActive = false;
                            this.$emit('activated', 'teams');
                        } else if (item == 'notif') {
                            this.teamsActive = false;
                            this.notifActive = true;
                            this.$emit('activated', 'notif');
                        }
                    }
                },
                watch: {
                    invitationsCount() {
                        if (this.$store.getters.invitationsCount)
                            this.getInvitationsCount = this.$store.getters.invitationsCount;
                        else
                            this.getInvitationsCount = 0;
                    },
                    unseenPMsCount() {
                        if (this.$store.getters.unseenPMsCount)
                            this.getUnseenPMsCount = this.$store.getters.unseenPMsCount;
                        else
                            this.getUnseenPMsCount = 0;
                    },
                    unseenMessagesCount() {
                        if (this.$store.getters.unseenMessagesCount)
                            this.getUnseenMessagesCount = this.$store.getters.unseenMessagesCount;
                        else
                            this.getUnseenMessagesCount = 0;

                    }
                },
                computed: {
                    ...mapGetters([
                            'getInvitations',
                            'invitationsCount',
                            'unseenPMsCount',
                            'unseenMessagesCount'
                    ])
                }

            }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .LeftItemB.item{
        width: 40%;
    }
    .LeftItemB.item.active{
        width: 60%;
    }

    .leftMenu{
        background-color: #fff;
    }
    .column{
        height: 100%;
    }


    .badge {
        display: block;
        position: relative;
        /*top: -12px;*/
        right: 3px;
        line-height: 16px;
        height: 16px;
        padding: 0 5px;
        font-family: Arial, sans-serif;
        text-shadow: 0 1px rgba(0, 0, 0, 0.25);
        border: 1px solid;
        border-radius: 10px;
        -webkit-box-shadow: inset 0 1px rgba(255, 255, 255, 0.3), 0 1px 1px rgba(0, 0, 0, 0.08);
        box-shadow: inset 0 1px rgba(255, 255, 255, 0.3), 0 1px 1px rgba(0, 0, 0, 0.08);
    }

    .badge.red {
        background: #fa623f;
        border-color: #fa5a35;
        background-image: -webkit-linear-gradient(top, #fc9f8a, #fa623f);
        background-image: -moz-linear-gradient(top, #fc9f8a, #fa623f);
        background-image: -o-linear-gradient(top, #fc9f8a, #fa623f);
        background-image: linear-gradient(to bottom, #fc9f8a, #fa623f);
    }
</style>
