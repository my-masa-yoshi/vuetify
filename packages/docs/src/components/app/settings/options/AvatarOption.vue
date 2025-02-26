<template>
  <v-defaults-provider
    :defaults="{
      VBadge: {
        color: 'primary',
        icon: 'mdi-check',
        offsetX: 6,
        offsetY: 6,
      }
    }"
  >
    <v-item-group>
      <v-row dense>
        <v-col cols="auto">
          <v-badge :model-value="user.avatar === auth0.user.value.picture">
            <v-avatar
              :image="auth0.user.value.picture"
              class="cursor-pointer"
              size="56"
              @click="onClick(auth0.user.value.picture)"
            />
          </v-badge>
        </v-col>

        <v-col
          v-for="(avatar, i) in avatars"
          :key="i"
          cols="auto"
        >
          <v-hover>
            <template #default="{ props: hoverProps, isHovering }">
              <v-badge :model-value="user.avatar === avatar">
                <v-avatar
                  v-bind="hoverProps"
                  :style="auth.isSubscriber ? {} : {
                    filter: isHovering ? 'grayscale(0%)' : 'grayscale(100%)',
                    opacity: isHovering ? '1' : '.12',
                  }"
                  size="56"
                  class="cursor-pointer"
                  @click="onClick(avatar)"
                >
                  <v-img :src="avatar">

                    <div
                      v-if="isHovering && !auth.isSubscriber"
                      class="d-flex align-center justify-center h-100"
                      @click.stop.prevent
                    >
                      <v-icon
                        color="white"
                        icon="mdi-lock"
                        size="small"
                      />
                    </div>
                  </v-img>
                </v-avatar>
              </v-badge>
            </template>
          </v-hover>
        </v-col>
      </v-row>
    </v-item-group>
  </v-defaults-provider>
</template>

<script setup>
  // Composables
  import { useAuth0 } from '@/plugins/auth'

  // Stores
  import { useAuthStore } from '@/store/auth'
  import { useUserStore } from '@/store/user'

  const auth0 = useAuth0()
  const auth = useAuthStore()
  const user = useUserStore()

  const avatars = [
    'https://cdn.vuetifyjs.com/docs/images/avatars/grass.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/wood.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/gold.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/planet.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/light.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/dark.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/blackguard.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/battlecruiser.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/blackhole.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/meteor.png',
    'https://cdn.vuetifyjs.com/docs/images/avatars/tada.png',
  ]

  function onClick (avatar) {
    user.avatar = avatar
  }
</script>
