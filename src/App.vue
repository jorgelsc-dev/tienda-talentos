<template>
  <v-app>
    <!-- App Bar -->
    <v-app-bar app color="deep-purple accent-4" dark elevation="4">
      <v-toolbar-title class="d-flex align-center">
        <!-- Imagen con relación de aspecto fija -->
        <v-avatar class="mr-2" size="250" tile>
          <v-img src="@/assets/2.png" max-height="80" max-width="210" :aspect-ratio="2" contain class="mr-2"></v-img>
        </v-avatar>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn href="https://wa.me/+5356605092?text=Info" icon><v-icon>mdi-whatsapp</v-icon></v-btn>
    </v-app-bar>

    <!-- Main Content -->
    <v-main>


      <v-container>
        <v-row>
          <v-col cols="12" md="6">
            <v-carousel cycle hide-delimiter-background>
              <v-carousel-item v-for="(slide, i) in promoSlides" :key="i" :src="slide.image" style="height: 100%;">
                <v-row class="fill-height" align="center" justify="center">
                  <div class="text-center">
                    <h2 class="text-white font-weight-bold text-h4">
                      {{ slide.title }}
                    </h2>
                    <p class="text-white">{{ slide.subtitle }}</p>
                  </div>
                </v-row>
              </v-carousel-item>
            </v-carousel>
          </v-col>
          <v-col cols="12" md="6">
            <v-container>
              <v-row>
                <v-col cols="12">
                  <v-card class="pa-0" elevation="0" style="background-color: transparent;">
                    <v-img src="@/assets/3.png" class="rounded-lg" cover height="300px">
                      <div class="d-flex flex-column fill-height justify-end px-4 py-6 text-black">
                        <v-card-title class="text-h4 font-weight-bold">Pide lo que quieras...</v-card-title>
                        <v-card-text class="font-weight-bold text-h6">¡por WhatsApp!</v-card-text>
                        <v-card-actions>
                          <v-btn class="bg-primary" color="primary" @click="dialog = true">
                            <p class="text-white">¿Cómo es el proceso?</p>
                          </v-btn>
                        </v-card-actions>
                      </div>
                    </v-img>
                  </v-card>

                  <!-- Modal / Dialog -->
                  <v-dialog v-model="dialog" max-width="400">
                    <v-card>
                      <v-card-item>
                        <v-container class="ma-5 pa-5">
                          <v-row>
                            <v-col cols="6">
                              <p class="text-center ma-5">1. Selecciona los productos</p>
                              <v-img src="@/assets/6.svg" height="100"></v-img>
                            </v-col>
                            <v-col cols="6">
                              <p class="text-center ma-5">2. Revisa y realiza tu pedido</p>
                              <v-img src="@/assets/7.svg" height="100"></v-img>
                            </v-col>
                          </v-row>
                          <v-row>
                            <v-col cols="6">
                              <p class="text-center ma-5">3. Confirma el pedido por WhatsApp</p>
                              <v-img src="@/assets/8.svg" height="100"></v-img>
                            </v-col>
                            <v-col cols="6">
                              <p class="text-center ma-5">4. Espera la entrega de tu pedido</p>
                              <v-img src="@/assets/9.svg" height="100"></v-img>
                            </v-col>
                          </v-row>
                        </v-container>

                      </v-card-item>
                      <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn text @click="dialog = false">Cerrar</v-btn>
                      </v-card-actions>
                    </v-card>
                  </v-dialog>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12" md="6">
                  <v-card class="pa-0" elevation="0" style="background-color: transparent;">
                    <v-img src="@/assets/23.png" class="rounded-lg" cover height="300px">
                      <div class="d-flex flex-column fill-height justify-end px-4 py-6">
                        <v-card-text>
                          <p class="font-weight-bold text-h4 text-white">Envíos</p>
                          <p class="font-weight-bold text-h4 text-white">para toda</p>
                          <p class="font-weight-bold text-h4 text-white">Cuba</p>
                        </v-card-text>
                      </div>
                    </v-img>
                  </v-card>
                </v-col>
                <v-col cols="12" md="6">
                  <v-card class="pa-0" elevation="0" style="background-color: transparent;">
                    <v-img src="@/assets/24.png" class="rounded-lg" cover height="300px">
                      <div class="d-flex flex-column fill-height justify-end px-4 py-6">
                        <v-card-title>
                          <p class="text-h4 font-weight-bold">Garantía</p>
                          <p class="text-h4 font-weight-bold">de 6</p>
                          <p class="text-h4 font-weight-bold">Meses</p>
                        </v-card-title>
                        <v-card-text>
                          <p class="font-weight-bold text-h6">Para</p>
                          <p class="font-weight-bold text-h6">todos los</p>
                          <p class="font-weight-bold text-h6">productos</p>
                        </v-card-text>
                      </div>
                    </v-img>
                  </v-card>
                </v-col>
              </v-row>
            </v-container>
          </v-col>
        </v-row>
      </v-container>
      <!-- Categorías -->
      <v-container class="text-center my-6">
        <v-row class="d-flex flex-row justify-center align-center flex-wrap">
          <v-btn v-for="cat in categories" :key="cat" class="ma-2 d-flex align-center"
            :color="cat === selectedCategory ? 'deep-purple accent-4' : 'grey lighten-2'" dark
            @click="selectedCategory = cat">
            <v-avatar size="24" class="mr-2">
              <v-img :src="categoryImages[cat]" />
            </v-avatar>
            {{ cat }}
          </v-btn>
        </v-row>
      </v-container>


      <!-- Productos -->
      <v-container class="py-6">
        <v-row>
          <v-col cols="12" md="3" v-for="product in filteredProducts" :key="product.id">
            <v-hover v-slot="{ props }">
              <v-card v-bind="props" :class="props.isHovering ? 'elevation-16' : 'elevation-4'"
                class="rounded-2xl transition-swing d-flex flex-column" style="height: 100%;">
                <v-img :src="product.image" :aspect-ratio="4 / 3" cover class="rounded-t-2xl"></v-img>
                <v-card-title class="text-h6 font-weight-medium px-4 pt-4 pb-2">
                  {{ product.name }}
                </v-card-title>
                <v-card-subtitle class="text-grey-darken-1 px-4 py-0">
                  {{ product.category }}
                </v-card-subtitle>
                <v-card-text class="px-4 pt-2 pb-0 flex-grow-1">
                  <div class="text-lg font-weight-bold mb-2">
                    ${{ product.price.toFixed(2) }}
                  </div>
                  <div class="text-sm text-grey">
                    {{ product.description }}
                  </div>
                </v-card-text>
                <v-card-actions>                  
                  <v-btn color="success" icon variant="flat" size="small" :href="whatsappLink(product)" target="_blank"
                    class="whatsapp-btn" style="position: absolute; bottom: 8px; right: 8px;">
                    <v-icon>mdi-whatsapp</v-icon>
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
    <v-footer app color="deep-purple accent-4" dark>
      <v-container class="text-center">
        <span>&copy; 2025 Tienda Talentos - Todos los derechos reservados</span>
      </v-container>
    </v-footer>
    <v-btn icon large color="success" class="whatsapp-fab"
      :href="`https://wa.me/+5356605092?text=${encodeURIComponent('Hola, necesito más información sobre CoolShop.')}`"
      target="_blank">
      <v-icon large>mdi-whatsapp</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      selectedCategory: 'Todos',
      products: [
        {
          id: 1,
          name: 'Split Milexus',
          category: 'Aires acondicionados',
          price: 380.00,
          image: require('@/assets/28.png'),
          description: 'Peso: 54 kg, Color: Blanco, Tamaño: 30,5 x 85,5 x 25,5 cm',
        },
        {
          id: 2,
          name: 'Televisor Kodak 43SVA1003BT',
          category: 'Televisores',
          price: 360.00,
          image: require('@/assets/29.jpg'),
          description: 'El televisor Kodak 43SVA1003BT es un modelo Smart TV con pantalla de 43 pulgadas, diseñado para ofrecer una experiencia de visualización inmersiva y características inteligentes a un precio accesible',
        },
        {
          id: 3,
          name: 'Televisor smart tv Royal RLED5524 KBT',
          category: 'Televisores',
          price: 600.00,
          image: require('@/assets/30.png'),
          description: 'El Smart TV Royal RLED5524 KBT  es un televisor inteligente con una pantalla de 55 pulgadas, diseñado para ofrecer una experiencia de entretenimiento de alta calidad',
        },
        {
          id: 4,
          name: 'LG 65 Inch Class UQ7070',
          category: 'Televisores',
          price: 1100.00,
          image: require('@/assets/31.png'),
          description: 'Especificaciones generales: Tamaño de pantalla: 65 pulgadas (diagonal). Resolución: 4K UHD (3840 x 2160 píxeles). Tipo de panel: LED. Procesador: α5 Gen5 AI Processor 4K, que mejora el contenido de baja resolución para acercarlo a calidad 4K. Sistema operativo: webOS 22, con una interfaz intuitiva y compatibilidad con aplicaciones de streaming como Netflix, Disney+, Prime Video, etc.',
        },
        {
          id: 5,
          name: 'SAMSUNG DU7200 65',
          category: 'Televisores',
          price: 1100.00,
          image: require('@/assets/32.png'),
          description: 'Tamaño de pantalla 	65 Pulgadas Marca 	SAMSUNG Tecnología de pantalla 	LCD Resolución 	4K Velocidad de actualización 	60 Hz Características especiales 	PurColor; Ampliación 4K; Motion Xcelerator; HDR; Crystal Processor 4K; Potenciador de contraste Componentes incluidos 	Blu-ray Tecnología de conectividad 	Wi-Fi Relación de aspecto 	16:09 Dimensiones del producto 	10,5″prof. x 57,2″an. x 34,6″al. pulgadas',
        },
        {
          id: 6,
          name: 'Kodak UHD 50 50SVA1003BT',
          category: 'Televisores',
          price: 520.00,
          image: require('@/assets/33.png'),
          description: 'Modelo: Kodak 50SVA1003BT Tipo de pantalla: LED Tamaño de pantalla: 50 pulgadas Resolución: 4K Ultra HD (3840 x 2160 píxeles) Relación de aspecto: 16:9 Tasa de refresco: 60 Hz Smart TV: Sí, con sistema operativo Android TV Conectividad: Wi-Fi: Integrado Bluetooth: Integrado Ethernet (LAN): Puerto disponible',
        },
        {
          id: 7,
          name: 'Televisor LG UHD 43UR73',
          category: 'Televisores',
          price: 460.00,
          image: require('@/assets/34.png'),
          description: 'Marca: LG Modelo: 43UR73 Tamaño de pantalla: 43 pulgadas Resolución: UHD 4K (3840 x 2160 píxeles)',
        },
        {
          id: 8,
          name: 'Philips Smart TV Roku Roku de 40 pulgadas',
          category: 'Televisores',
          price: 400.00,
          image: require('@/assets/35.jpg'),
          description: 'El televisor Philips Roku con tecnología de pantalla LED de última generación le ofrece una resolución FHD de pantalla ancha de 1920 x 1080p píxeles. Produce imágenes de escaneo progresivo sin parpadeo brillantes con un brillo óptimo y colores excelentes. Mejore su experiencia de visualización con imágenes más nítidas y colores bellamente vibrantes.',
        },
        {
          id: 9,
          name: 'Televisor 4K Milexus LED Smart de 55',
          category: 'Televisores',
          price: 460.00,
          image: require('@/assets/35.png'),
          description: 'Disfruta de una experiencia visual excepcional con el televisor 4K Milexus LED Smart de 55». Con una resolución de pantalla 4K y sistema digital ISDBT, este televisor ofrece una calidad de imagen asombrosa. Equipado con Android 11, Bluetooth y WIFI, este televisor inteligente te brinda acceso a una amplia gama de aplicaciones y contenido en línea. Las múltiples opciones de conectividad, como 2 puertos USB, 2 entradas HDMI, y otras entradas, te permiten conectar tus dispositivos con facilidad. Con una fuente de alimentación de AC-100-240V-50/60Hz y especificaciones potentes como 3.5 GB de almacenamiento y 8 GB de memoria, este televisor Milexus es una combinación perfecta de rendimiento y entretenimiento.',
        },
        {
          id: 10,
          name: 'OSKA TV 32¨ Smart tv',
          category: 'Televisores',
          price: 230.00,
          image: require('@/assets/36.png'),
          description: 'La TV VM-LED-32-ISDBT es un televisor LED de 32 pulgadas que ofrece una experiencia visual envolvente y de alta calidad. Con una resolución nítida y colores vibrantes, este televisor es ideal para disfrutar de tus programas, películas y juegos favoritos. Equipado con sintonizador ISDB-T, te permite acceder a una variedad de canales digitales para entretenimiento ilimitado. Su diseño elegante y compacto lo convierte en una adición perfecta para cualquier espacio.',
        },
        {
          id: 11,
          name: 'Oska Smart Tv 32¨ OSK32DBVT',
          category: 'Televisores',
          price: 230.00,
          image: require('@/assets/37.png'),
          description: 'Tamaño de pantalla: 32 pulgadas Resolución: 1366 x 768 píxeles (HD Ready) Tipo de panel: LED Sistema operativo: Android 12 Procesador: Quad-core Memoria RAM: 2GB Almacenamiento interno: 16GB Conectividad: WiFi 802.11 b/g/n, Bluetooth 5.0 Puertos: HDMI x 2, USB x 2, Ethernet, entrada AV, salida de auriculares Dimensiones (sin soporte): 72.6 x 43.1 x 8.1 cm Peso (sin soporte): 5.2 kg Incluye: 2 controles remotos, cable de alimentación, manual de usuario',
        },
        {
          id: 12,
          name: 'Ventilador JINGHAN industrial',
          category: 'Ventiladores',
          price: 100.00,
          image: require('@/assets/38.png'),
          description: 'Ventilador Industrial de Hierro',
        },
        {
          id: 13,
          name: 'Ventilador de pie Hurricane Home',
          category: 'Ventiladores',
          price: 100.00,
          image: require('@/assets/39.png'),
          description: 'El ventilador de pie Hurricane Home combina funcionalidad y bienestar en un elegante diseño blanco. Con características innovadoras como difusor de aromaterapia y tecnología de generación de iones negativos, este ventilador no solo refresca tu espacio, sino que también ayuda a limpiar y purificar el aire que respiras. Con 3 velocidades y modos de viento ajustables, incluyendo normal, brisa y sueño, este ventilador ofrece un ambiente fresco y relajante en tu hogar. Controla todas estas funciones de forma conveniente a través del panel de control o el mando a distancia',
        },
        {
          id: 14,
          name: 'Ventilador de piso Hurricane',
          category: 'Ventiladores',
          price: 100.00,
          image: require('@/assets/40.png'),
          description: 'El ventilador de piso Hurricane de 16″ de bajo consumo de energía es la combinación perfecta de eficiencia y rendimiento. Con un diseño elegante y un funcionamiento silencioso, este ventilador es ideal para mantener tu hogar fresco y cómodo durante todo el año. La eficiencia energética de 16 pulgadas garantiza un flujo de aire constante y potente, mientras que su estilo moderno complementa cualquier espacio, desde la sala de estar hasta la oficina.',
        },
        {
          id: 15,
          name: 'Ventilador de piso Jinghan',
          category: 'Ventiladores',
          price: 100.00,
          image: require('@/assets/41.png'),
          description: 'El ventilador de piso Jinghan es la solución perfecta para mantener tu espacio fresco y cómodo en los días calurosos. Con un diseño elegante y eficiente, este ventilador combina potencia y funcionalidad para brindarte un flujo de aire refrescante en cualquier habitación. Con características como múltiples velocidades, ajuste de inclinación y un funcionamiento silencioso, el ventilador de piso Jinghan es una adición imprescindible para tu hogar u oficina.',
        },
        {
          id: 16,
          name: 'Household Microwave Oven jvm6175dk5ww',
          category: 'Hornos y microondas',
          price: 250.00,
          image: require('@/assets/42.png'),
          description: 'El Over-the-Range Sensor Microwave Oven Model JVM6175DKWW de GE Appliances',
        },
        {
          id: 17,
          name: 'Panasonic NN-SB428S – Horno microondas',
          category: 'Hornos y microondas',
          price: 150.00,
          image: require('@/assets/43.png'),
          description: 'Marca: Panasonic Modelo: NN-SB428S Tipo de microondas: De encimera',
        },

        {
          id: 18,
          name: 'Licuadora Oska OSK999PL',
          category: 'Batidoras, Licuadoras y Moledoras',
          price: 60.00,
          image: require('@/assets/44.png'),
          description: 'Marca: Oska Modelo: OSK999PL',
        },
        {
          id: 19,
          name: 'Licuadora 2 velocidades DURAPRO',
          category: 'Batidoras, Licuadoras y Moledoras',
          price: 80.00,
          image: require('@/assets/45.png'),
          description: 'La licuadora de 2 velocidades DURAPRO Modelo BLBD202GW es un electrodoméstico de cocina versátil y eficiente diseñado para satisfacer las necesidades de los hogares modernos. Con su potente motor y un vaso resistente de 1,25 litros de capacidad, esta licuadora puede procesar una amplia variedad de ingredientes con facilidad, desde frutas y verduras hasta hielo y mezclas congeladas.',
        },

        {
          id: 20,
          name: 'Olla Arrocera Eléctrica CFXB-1.8 EKO',
          category: 'Ollas, Parrillas y Sartenes',
          price: 60.00,
          image: require('@/assets/46.png'),
          description: 'Marca: Generalmente, este tipo de modelo es genérico, pero tiene características comunes de ollas arroceras eléctricas.',
        },
        {
          id: 21,
          name: 'Olla eléctrica multifuncional Eko',
          category: 'Ollas, Parrillas y Sartenes',
          price: 100.00,
          image: require('@/assets/47.png'),
          description: 'Marca: Eko Modelo: YBXB-6EKO',
        },
        {
          id: 22,
          name: 'Refrigerador Samsung RT32A500JS8 11.5p',
          category: 'Refrigeradores',
          price: 860.00,
          image: require('@/assets/48.png'),
          description: 'El refrigerador Samsung RT32A500JS8 es un modelo de doble puerta con congelador superior, diseñado para ofrecer eficiencia energética y un rendimiento de refrigeración óptimo',
        },
        {
          id: 23,
          name: 'Refrigerador LG VT29WPP',
          category: 'Refrigeradores',
          price: 850.00,
          image: require('@/assets/49.png'),
          description: 'Capacidad: Aproximadamente 260 – 300 litros, ideal para familias pequeñas o medianas. Tipo de refrigerador: Top Freezer, con congelador en la parte superior y refrigerador en la parte inferior. Sistema de enfriamiento: Tecnología No Frost, lo que significa que no requiere descongelamiento manual y distribuye el frío de manera uniforme. Eficiencia energética: Clasificación de eficiencia energética A+ o superior, lo que garantiza un consumo reducido de electricidad. Control de temperatura: Termostato ajustable manual o digital para un control preciso de la temperatura. Tecnología de compresor: Compresor Inverter, que optimiza el rendimiento y ahorra energía ajustando la potencia según las necesidades de refrigeración',
        },
        {
          id: 24,
          name: 'Refrigerador Samsung 15 pie RT42DG67345',
          category: 'Refrigeradores',
          price: 1150.00,
          image: require('@/assets/50.png'),
          description: 'Samsung RT42DG67345 es un modelo de tipo combinado (congelador en la parte superior) que ofrece varias características destacadas. Algunas de sus especificaciones son: Capacidad: Aproximadamente 400-450 litros, ideal para familias medianas. Tecnología de enfriamiento: Twin Cooling Plus: Sistema de doble enfriamiento que permite mantener los niveles de humedad en el refrigerador y el congelador por separado, lo que ayuda a que los alimentos se conserven frescos por más tiempo. Eficiencia energética: Clasificación A+ o A++, dependiendo de la región, lo que asegura un bajo consumo de energía.',
        },
        {
          id: 25,
          name: 'Refrigerador Premier NV-8430D2D107TN1',
          category: 'Refrigeradores',
          price: 750.00,
          image: require('@/assets/51.png'),
          description: 'nombre: nevera 302l/10pc (f). acero inoxidable, c/dispensador de agua. Referencia: nv-8430D2D107. Capacidad: 302 litros/10.7 pie cubicos. Tipo: escarcha. Número de puertas: 2. Color y diseño: acero inoxidable, c/dispensador de agua. Dimensiones:  600×590×1720mm (wxdxh)',
        },
        {
          id: 26,
          name: 'Refrigerador Milexus ML-RF-INOX-6.5CUFT',
          category: 'Refrigeradores',
          price: 480.00,
          image: require('@/assets/52.png'),
          description: 'Milexus ML-RF-INOX-6.5CUFT ofrece características que lo hacen adecuado para espacios pequeños, combinando funcionalidad y diseño moderno.',
        },
        {
          id: 27,
          name: 'Refrigerador Royal RF11SWD',
          category: 'Refrigeradores',
          price: 750.00,
          image: require('@/assets/53.png'),
          description: 'Marca: Royal. Modelo: RF11SWD. Capacidad: 11 pies cúbicos',
        },
        {
          id: 28,
          name: 'Refrigerador LG 13.2 VT38WPP',
          category: 'Refrigeradores',
          price: 1100.00,
          image: require('@/assets/54.png'),
          description: 'Marca: LG. Modelo: VT38WPP. Capacidad: 13.2 pies cúbicos',
        },
        {
          id: 29,
          name: 'Refrigerador Milexus ML-RFWD-13.1 CUFT-DD',
          category: 'Refrigeradores',
          price: 850.00,
          image: require('@/assets/55.png'),
          description: 'Marca: Milexus. Modelo: ML-RFWD-13.1 CUFT-DD. Capacidad: 13.1 pies cúbicos',
        },
        {
          id: 30,
          name: 'Refrigerador BLAUPUNKT 15.4 P BKFR004',
          category: 'Refrigeradores',
          price: 1100.00,
          image: require('@/assets/56.png'),
          description: 'Marca: Blaupunkt. Modelo: BKFR004. Capacidad: 15.4 pies cúbicos. Color: Acero inoxidable (acabado metálico)',
        },
        {
          id: 31,
          name: 'Refrigerador Milexus',
          category: 'Refrigeradores',
          price: 700.00,
          image: require('@/assets/57.png'),
          description: 'El refrigerador Milexus de 7 pies es una solución compacta y eficiente para el almacenamiento de alimentos en espacios más reducidos. Con un diseño moderno y funcional, este refrigerador ofrece un equilibrio perfecto entre tamaño y capacidad, ideal para hogares con necesidades de almacenamiento más modestas. A pesar de su tamaño más pequeño, este refrigerador garantiza un rendimiento confiable y mantiene tus alimentos frescos y organizados.',
        },
        {
          id: 32,
          name: 'Refrigerador LG de 17 pies con 2 puertas',
          category: 'Refrigeradores',
          price: 1440.00,
          image: require('@/assets/58.png'),
          description: 'La nevera LG de 17 pies cúbicos en color plateado con 2 puertas ofrece un amplio espacio de almacenamiento con un diseño elegante y funcional. Con características de alta calidad y un interior bien organizado, esta nevera proporciona una solución eficiente para mantener tus alimentos frescos y bien conservados. Sus dos puertas facilitan el acceso a los compartimentos del refrigerador y el congelador, mientras que su color plateado agrega un toque moderno a tu cocina.',
        },
        {
          id: 33,
          name: 'Refrigerador LG de 7 pies',
          category: 'Refrigeradores',
          price: 650.00,
          image: require('@/assets/59.png'),
          description: 'Marca: LG. Modelo: GU21WPP. Capacidad: 7 pies cúbicos.',
        },
        {
          id: 34,
          name: 'Refrigerador Galanz 7.6 pies (modelo retro)',
          category: 'Refrigeradores',
          price: 600.00,
          image: require('@/assets/60.png'),
          description: 'Certificado Energy Star | El sistema de control de temperatura analógico ajustable ofrece diferentes ajustes de temperatura, lo que te da un gran control sobre la temperatura interior | Los estantes de vidrio para nevera proporcionan un fácil almacenamiento y una fácil limpieza.',
        },
        {
          id: 35,
          name: 'Nevera Royal 7.8P RFH78',
          category: 'Congeladores y Freezers',
          price: 400.00,
          image: require('@/assets/61.png'),
          description: 'Capacidad total: Aproximadamente 300 a 400 litros (dependiendo de la versión), ideal para familias medianas y grandes. Refrigerador y congelador combinados, con suficiente espacio para almacenar alimentos frescos y congelados.',
        },
        {
          id: 36,
          name: 'Nevera-XINGX',
          category: 'Congeladores y Freezers',
          price: 550.00,
          image: require('@/assets/62.png'),
          description: 'Marca: Xingx. Capacidad: 10.9 pies cúbicos (equivalente a unos 308 litros), ideal para familias pequeñas o medianas, ofreciendo suficiente espacio para almacenar alimentos frescos y congelados.',
        },
        {
          id: 37,
          name: 'Nevera Royal 5.5 pies',
          category: 'Congeladores y Freezers',
          price: 400.00,
          image: require('@/assets/63.png'),
          description: 'La Nevera de 5.5 Pies Marca Reyan es un electrodoméstico de refrigeración compacto y eficiente, ideal para espacios reducidos como oficinas, dormitorios o pequeñas cocinas. Con unas dimensiones de 18.5 x 19.7 x 33.5 pulgadas, este modelo ofrece un volumen total de 5.5 pies cúbicos, lo que lo convierte en una solución ideal para aquellos que requieren una nevera de capacidad media sin ocupar demasiado espacio.',
        },
        {
          id: 38,
          name: 'Exhibidor Vertical triple XINGX',
          category: 'Congeladores y Freezers',
          price: 1900.00,
          image: require('@/assets/64.png'),
          description: 'El Exhibidor Vertical Doble XINGX de 25 pies cúbicos / 690 litros es un sistema de exhibición y refrigeración de alto rendimiento, diseñado para satisfacer las necesidades de almacenamiento y presentación de una amplia variedad de productos. Con unas dimensiones generales de 1165 x 640 x 2020 mm, este exhibidor vertical ofrece un volumen total de 25 pies cúbicos / 690 litros, lo que lo convierte en una opción ideal para negocios que requieren una gran capacidad de almacenamiento y exhibición.',
        },
        {
          id: 39,
          name: 'Nevera horizontal Marca Milexus de 3.5 pies',
          category: 'Congeladores y Freezers',
          price: 290.00,
          image: require('@/assets/65.png'),
          description: 'La nevera horizontal Marca Milexus de 3.5 pies en color gris es un electrodoméstico versátil y eficiente diseñado para satisfacer las necesidades de almacenamiento de alimentos en hogares y espacios pequeños. Con un volumen interior de 3.5 pies cúbicos, esta nevera ofrece un espacio de almacenamiento generoso, lo que la convierte en una opción ideal para solteros, parejas o familias con requisitos de espacio limitados.',
        },
        {
          id: 40,
          name: 'Equipo de audio LG',
          category: 'Equipos de Sonido',
          price: 250.00,
          image: require('@/assets/66.png'),
          description: '',
        },
        {
          id: 41,
          name: 'Bocina Premier de 40,000 W',
          category: 'Equipos de Sonido',
          price: 250.00,
          image: require('@/assets/67.png'),
          description: 'La Bocina Premier de 40,000 W es un altavoz de alta potencia diseñado para ofrecer un rendimiento de sonido excepcional en grandes espacios y eventos. Con una impresionante capacidad de 40,000 W, esta bocina está construida con los más avanzados componentes y tecnologías de audio para brindar una experiencia acústica envolvente y de alta fidelidad.',
        },
        {
          id: 42,
          name: 'Empava cocina EMPV-30GC26',
          category: 'Cocinas eléctricas y de gas',
          price: 300.00,
          image: require('@/assets/68.png'),
          description: 'Marca: Empava. Modelo: EMPV-30GC26. Tipo de cocina: Encimera de gas de 5 quemadores',
        },
        {
          id: 43,
          name: 'Cocina de Gas Oasis OS-G22C',
          category: 'Cocinas eléctricas y de gas',
          price: 90.00,
          image: require('@/assets/69.png'),
          description: 'Marca: Oasis. Modelo: OS-G22C. Tipo de cocina: Cocina de gas de 2 quemadores',
        },
        {
          id: 44,
          name: 'Cocina milexus ml eg 4q 900',
          category: 'Cocinas eléctricas y de gas',
          price: 350.00,
          image: require('@/assets/70.png'),
          description: 'Marca: Milexus. Modelo: ML-EG-4Q-900. Color: Acero inoxidable (plateado).',
        },
        {
          id: 45,
          name: 'Cocina Milexus ML-CG-6Q-600',
          category: 'Cocinas eléctricas y de gas',
          price: 540.00,
          image: require('@/assets/71.png'),
          description: 'Marca: Milexus. Modelo: ML-CG-6Q-600. Color: Negra.',
        },
        {
          id: 46,
          name: 'Cocina de inducción OSKA',
          category: 'Cocinas eléctricas y de gas',
          price: 70.00,
          image: require('@/assets/72.png'),
          description: 'Plato Cerámico: El plato de cocción está hecho de cerámica, un material resistente y fácil de limpiar. Esta superficie cerámica es lisa y brillante, lo que facilita la limpieza después de cocinar. Tamaño de 250 x 250 mm: Las dimensiones del plato de cocción son 250 milímetros de largo por 250 milímetros de ancho, lo que proporciona un espacio de cocción adecuado para la mayoría de utensilios de cocina.',
        },
        {
          id: 47,
          name: 'Empava Cocina de gas de 24 pulgadas',
          category: 'Cocinas eléctricas y de gas',
          price: 300.00,
          image: require('@/assets/73.png'),
          description: 'Empava Placa de cocina de gas de 24″ en vidrio templado negro con 4 quemadores 24XGC28. Marca: Empava. Fuente de alimentación: Gas. Tipo de combustible: Gas. Características especiales: Ideal para cocinar, ideal para Acción de Gracias, Navidad y otras celebraciones, excelente como regalo o para remodelación/Flip House. Material: Vidrio. Dimensiones: 20,08″ de profundidad x 23,23″ de ancho x 3,94″ de alto. Tipo de quemador: Hierro fundido. Tipo de sistema de encendido: Electrónico.',
        },

        {
          id: 48,
          name: 'Lavadora Milexus 9kg ML-WM-9KGS',
          category: 'Lavadoras/Secadoras',
          price: 290.00,
          image: require('@/assets/74.png'),
          description: 'La lavadora Milexus de 9 kg, modelo ML-WM-9KGS es un electrodoméstico diseñado para uso doméstico, con capacidad media y varias características que la hacen eficiente.',
        },
        {
          id: 49,
          name: 'Lavadora frigidaire 12kg FWTM12M3BTW',
          category: 'Lavadoras/Secadoras',
          price: 430.00,
          image: require('@/assets/75.png'),
          description: 'Marca: FRIGIDAIRE. Modelo: FWTM12M3BTW. Categoría:HOGAR. Clase: LAVADORA SEMIAUTOMÁTICA. Caracteristicas: 12Kg.',
        },
        {
          id: 50,
          name: 'Lavadora Samsung 9 kg WA90CG4240BY',
          category: 'Lavadoras/Secadoras',
          price: 480.00,
          image: require('@/assets/76.png'),
          description: 'Modelo: WA90CG4240BY. Capacidad de lavado: 9 kg. Tipo de lavadora: Carga superior. Dimensiones: Alto: Aproximadamente 100 cm. Ancho: 54 cm. Profundidad: 56 cm. Peso: Aproximadamente 31 kg.',
        },
        {
          id: 51,
          name: 'Lavadora Challenger CH-WM810 de 8 kg',
          category: 'Lavadoras/Secadoras',
          price: 320.00,
          image: require('@/assets/77.jpg'),
          description: 'Marca: Challenger. Modelo: CH-WM810. Capacidad: 8 kg (ideal para familias pequeñas o medianas).',
        },
        {
          id: 52,
          name: 'Lavadora Royal RWA090',
          category: 'Lavadoras/Secadoras',
          price: 420.00,
          image: require('@/assets/78.jpg'),
          description: 'Marca: Royal. Modelo: RWA090. Tipo de lavadora: Automática de carga superior.',
        },
        {
          id: 53,
          name: 'Lavadora automática konka 5kg',
          category: 'Lavadoras/Secadoras',
          price: 380.00,
          image: require('@/assets/79.png'),
          description: 'La lavadora automática Milexus de 8 Kg es la solución perfecta para tus necesidades de lavado. Con una capacidad de lavado de 8 Kg, esta lavadora ofrece un rendimiento excepcional para mantener tu ropa impecable. Con 10 programas de lavado, incluido un ciclo personalizable, podrás cuidar tus prendas de la mejor manera posible. El modelo ML-LVTL-8KG de Milexus cuenta con una potencia de 300-400 W y funciona a 110V/60Hz. Con dimensiones de 560 x 578 x 942 mm, esta lavadora automática es compacta y eficiente. Además, viene con una garantía de 30 días para tu tranquilidad.',
        }
      ],
      categoryImages: {
        Todos: require('@/assets/25.png'),
        'Aires acondicionados': require('@/assets/10.png'),
        Televisores: require('@/assets/11.png'),
        Ventiladores: require('@/assets/12.png'),
        Refrigeradores: require('@/assets/13.png'),
        'Congeladores y Freezers': require('@/assets/14.png'),
        'Batidoras, Licuadoras y Moledoras': require('@/assets/15.png'),
        'Lavadoras/Secadoras': require('@/assets/16.png'),
        'Electrodomésticos pequeños': require('@/assets/17.png'),
        'Cocinas eléctricas y de gas': require('@/assets/18.png'),
        'Equipos de Sonido': require('@/assets/19.png'),
        'Hornos y microondas': require('@/assets/20.png'),
        'Ollas, Parrillas y Sartenes': require('@/assets/21.png'),
        Otros: require('@/assets/22.png'),
      },

      promoSlides: [
        {
          image: require('@/assets/25.png'),
          title: 'Estilo Vintage en tu Hogar',
          subtitle: 'Descubre el Encanto Retro con el Refrigerador Galanz Exclusivo',
        },
        {
          image: require('@/assets/26.png'),
          title: 'Eleva tu Hogar',
          subtitle: 'con Tecnología Avanzada',
        },
        {
          image: require('@/assets/27.png'),
          title: 'Todo para tu cocina ',
          subtitle: 'Consulta todas nuestras ofertas',
        },
      ],
    };
  },
  computed: {
    categories() {
  const all = ['Todos'];
  const uniqueSet = new Set(this.products.map(p => p.category));
  const uniqueArray = Array.from(uniqueSet);
  const additionalCategories = []
  return all.concat(uniqueArray, additionalCategories);
},
    filteredProducts() {
      if (this.selectedCategory === 'Todos') return this.products;
      return this.products.filter(p => p.category === this.selectedCategory);
    },
  },
  methods: {
    addToCart(product) {
      alert(`${product.name} fue añadido al carrito.`);
    },
    whatsappLink(product) {
      const number = '+5356605092';
      const message = `Hola, estoy interesado en el producto: ${product.name}, categoría: ${product.category}, precio: $${product.price}`;
      return `https://wa.me/${number}?text=${encodeURIComponent(message)}`;
    },
  },
};
</script>

<style scoped>
body {
  font-family: 'Poppins', sans-serif;
  background-color: #f5f5f5;
}

.v-card {
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.v-card:hover {
  transform: translateY(-5px);
}

.v-img {
  object-fit: cover;
}

.v-btn {
  border-radius: 12px;
}

/* Botón flotante de WhatsApp */
.whatsapp-fab {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 999;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}
</style>
