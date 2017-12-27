<template lang='pug'>
  #app
    div#select
      input.input(type='text' v-model='nombre' placeholder="Tu Nombre")
      .select
        select#cursoBasico(v-model='cursos[0]')
          option(value='0') El mas basico
          option(v-for='i in insignias' :value='i.id') {{i.curso}}
      .select
        select#cursoBasico(v-model='cursos[1]')
          option(value='0') El que mas te gusta
          option(v-for='i in insignias' :value='i.id') {{i.curso}}
      .select
        select#cursoBasico(v-model='cursos[2]')
          option(value='0') Otro basico que complemente
          option(v-for='i in insignias' :value='i.id') {{i.curso}}
      .select
        select#cursoBasico(v-model='cursos[3]')
          option(value='0') Tecnologia en que te centraste
          option(v-for='i in insignias' :value='i.id') {{i.curso}}
      .select
        select#cursoBasico(v-model='cursos[4]')
          option(value='0') La version profesional
          option(v-for='i in insignias' :value='i.id') {{i.curso}}
      .select
        select#cursoBasico(v-model='cursos[5]')
          option(value='0') Especializate
          option(v-for='i in insignias' :value='i.id') {{i.curso}}
      .select
        select#cursoBasico(v-model='cursos[6]')
          option(value='0') Profundiza y refuerza
          option(v-for='i in insignias' :value='i.id') {{i.curso}}

      button.button.is-success.is-inverted(v-on:click='canvas') Crear ruta!

      a#descarga.button(v-on:click='download') Descargar

    div#canvas
      img#ruta(width='1080', height='1080', :src='img', alt='Ruta', hidden='')
      canvas#myCanvas.level(width='900', height='1040', style='border:1px solid #d3d3d3;')
          | Your browser does not support the HTML5 canvas tag.
    div#images
      img(id='basico' width='180', height='180' :src='cursoBasico' hidden )
      img(id='gusta' width='180', height='180' :src='cursoGusto' hidden )
      img(id='complemento' width='180', height='180' :src='complemento' hidden )
      img(id='tecnologia' width='180', height='180' :src='tecnologia' hidden )
      img(id='profesional' width='180', height='180' :src='profesional' hidden )
      img(id='especializate' width='180', height='180' :src='especializate' hidden )
      img(id='profundiza' width='180', height='180' :src='profundiza' hidden )
    br
    br
</template>

<script>
import badges from '@/helpers/badges'
import insignias from '@/helpers/insignias'

export default {
  name: 'ruta-platzi',
  data () {
    return {
      badges,
      insignias,
      img: require('@/assets/rutas/ruta_profesional.png'),
      cursos: [0, 0, 0, 0, 0, 0, 0],
      bad: [0, 1, 2, 3, 4, 5, 6],
      nombre: '',
      imgData: null
    }
  },
  methods: {
    canvas: function () {
      console.log(this.cursos)
      var isrendering = true
      const nombre = this.nombre
      var canvas = document.getElementById('myCanvas')
      var ctx = canvas.getContext('2d')
      ctx.clearRect(0, 0, canvas.width, canvas.height)
      var img = document.getElementById('ruta')
      ctx.drawImage(img, 0, 0)

      // Nivel de insignia
      for (var b = 0; b < badges.length; b++) {
        var element = badges[b]
        const bg = document.getElementById(element.value)
        ctx.font = '15px Arial'
        ctx.textAlign = 'center'
        ctx.drawImage(bg, element.x, element.y)
        // ctx.fillText(cursos[b], (element.x + 80), (element.y + 180))

        // Insignia
        for (var i = 0; i < this.insignias.length; i++) {
          if (this.insignias[i].id === this.cursos[b]) {
            /// ///////
            var elemento = this.insignias[i].curso
            // ctx.fillText(elemento, (element.x + 80), (element.y + 180))
            /// //////
            var lines = elemento.split('\n')
            var lineheight = 15
            for (var z = 0; z < lines.length; z++) {
              ctx.fillText(lines[z], (element.x + 80), (element.y + 180) + (z * lineheight))
            }
            /// //////
            break
          }
        }

        // Nombre
        if (isrendering) {
          ctx.font = 'bold 30px Arial'
          ctx.textAlign = 'center'
          ctx.fillText(nombre, (canvas.width * 0.82), (canvas.height * 0.24))
          isrendering = false
        }
      }
    },
    download: function () {
      var canvas = document.getElementById('myCanvas')
      var a = document.getElementById('descarga')
      a.download = 'Ruta_Platzi.png'
      a.href = canvas.toDataURL('image/png').replace('image/png', 'image/octet-stream')
    }
  },
  computed: {
    cursoBasico () {
      let img
      let curso = this.cursos[0]
      if (parseInt(curso) === 0) {
        img = badges[0].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    },
    cursoGusto () {
      let img
      let curso = this.cursos[1]
      if (parseInt(curso) === 0) {
        img = badges[1].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    },
    complemento () {
      let img
      let curso = this.cursos[2]
      if (parseInt(curso) === 0) {
        img = badges[2].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    },
    tecnologia () {
      let img
      let curso = this.cursos[3]
      if (parseInt(curso) === 0) {
        img = badges[3].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    },
    profesional () {
      let img
      let curso = this.cursos[4]
      if (parseInt(curso) === 0) {
        img = badges[4].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    },
    especializate () {
      let img
      let curso = this.cursos[5]
      if (parseInt(curso) === 0) {
        img = badges[5].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    },
    profundiza () {
      let img
      let curso = this.cursos[6]
      if (parseInt(curso) === 0) {
        img = badges[6].src
      } else {
        for (var b = 0; b < insignias.length; b++) {
          if (curso === insignias[b].id) {
            img = insignias[b].img
          }
        }
      }
      return img
    }
  },
  mounted:
    function () {
      window.onload = function () {
        var canvas = document.getElementById('myCanvas')
        var ctx = canvas.getContext('2d')
        var img = document.getElementById('ruta')
        ctx.drawImage(img, 0, 0)

        for (var b = 0; b < badges.length; b++) {
          var element = badges[b]
          const bg = document.getElementById(element.value)
          ctx.drawImage(bg, element.x, element.y)
        }
      }
    }
}
</script>

<style>

</style>
