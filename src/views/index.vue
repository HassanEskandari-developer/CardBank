<script>
export default {
    data() {
        return {
            img: "images/bg-main-desktop.png",
            img1: "images/bg-main-mobile.png",
            imgCardName: "/images/bg-card-front.png",
            imgBack: "/images/bg-card-back.png",
            cardNumber: "",
            MM: "",
            YY: "",
            nameCard: "",
            cvCard: "",

        }
    },

    watch: {
        cardNumber: function (newVal) {

            if (this.cardNumber.length > 19) {
                // this.cardNumber=this.cardNumber.charAt(this.cardNumber.length-1)
                this.cardNumber = newVal.slice(0, 19)
            }
        },

        MM: function (newVal) {

            if (this.MM > 12) {
                this.MM = 12
            }
            if (this.MM != '00' && this.MM.toString().length > 2) {
                this.MM = newVal.toString().slice(0, 2)
            }
        },
        YY: function (newVal) {

            setTimeout(() => {
                if (this.YY < 24) {
                    this.YY = 24
                }
            }, "500");


            if (this.YY.toString().length > 2) {
                this.YY = newVal.toString().slice(0, 2)
            }
        },
        nameCard: function (newVal) {
            if (this.nameCard == '') {
                alert('adam bash poooor kon');
            }
            if (this.nameCard.length > 20) {

                this.nameCard = newVal.slice(0, 20)
            }
        },

        cvCard: function (newVal) {
            if (this.cvCard.toString().length > 4) {
                this.cvCard = newVal.toString().slice(0, 4)
            }
        }



    },
    methods: {

        cNumbr(e) {
            // null 0 '' undefined
            if (!this.cardNumber) {
                this.cardNumber = ''
            } else {
                let valuOfInput = this.cardNumber.toString().replaceAll(" ", "")
                if (this.cardNumber.length > 14) {
                    this.cardNumber = valuOfInput.replace(/(\d{4})(\d{4})(\d{4})(\d{0,4})/, "$1 $2 $3 $4")

                } else if (this.cardNumber.length > 9) {
                    this.cardNumber = valuOfInput.replace(/(\d{4})(\d{4})(\d{0,4})/, "$1 $2 $3")
                } else if (this.cardNumber.length > 4) {
                    this.cardNumber = valuOfInput.replace(/(\d{4})(\d{0,4})/, "$1 $2");
                } else {
                    this.cardNumber = valuOfInput
                }
            }
        },

        cardNumberNme(e) {
            let x = e.which || e.keycode
            if (x >= 48 && x <= 57) {
                return true
            } else {
                e.preventDefault();
                return false
            }
        }
    },
}
</script>




<template>
    <main>
        <section class="w-full h-[100vh] lg:flex ">
            <div class="w-full lg:w-1/4  relative">
                <img class="hidden lg:flex" :src="img" alt="">
                <img class="h-[30rem]  lg:hidden" :src="img1" alt="">

                <!-- //////////////////////cardname/////////////////////// -->
                <div
                    class="lg:w-[480px] w-[330px] h-[190px] lg:h-[250px] grid absolute top-0 left-[20px] lg:top-[140px] lg:left-[190px] bg-[url('/images/bg-card-front.png')] bg-contain bg-no-repeat rounded-[10px]">

                    <div class="flex w-[100px] h-[100px] justify-center items-center gap-3">
                        <div class="w-12 h-12 rounded-full bg-white"></div>
                        <div class="w-5 h-5 rounded-full border"></div>
                    </div>
                    <div class="w-full text-center">
                        <span class="text-white text-[30px] font-bold ">{{ cardNumber }}</span>
                    </div>

                    <div class="w-full flex  gap-12">
                        <div class=" w-2/4 text-center">
                            <span class="font-bold">{{ nameCard }}</span>
                        </div>

                        <div class="w-1/4 text-end">
                            <h2 class="font-bold ">
                                <span>
                                    <span v-if="MM && MM < 10">0</span>{{ MM }}
                                </span>
                                / {{ YY }}
                            </h2>
                        </div>
                    </div>

                </div>
                <!-- //////////////////cardback//////////////////// -->

                <div
                    class="lg:w-[480px] w-[330px]   h-[250px] absolute top-[14rem] left-[1.2rem]   lg:top-[410px] lg:left-[290px]  lg:flex bg-[url('/images/bg-card-back.png')] bg-contain bg-no-repeat rounded-[10px]">

                    <span class="absolute font-bold top-[76px] right-[50px] lg:top-[115px] lg:right-[80px]">{{ cvCard
                    }}</span>
                </div>

            </div>

            <!-- /////////////////////////input//////////////////////////////// -->


            <div class="w-full  lg:w-3/4 space-y-10 h-full  flex flex-col lg:justify-center items-center !py-5">
                <div class="flex flex-col justify-center items-center w-full   gap-3 ">
                    <div class="flex flex-col">
                        <span>full Name</span>
                        <input type="text"
                            class="border border-gray-300 lg:w-[500px]  w-[300px] h-[50px] rounded-[12px] placeholder:p-3 !px-6"
                            placeholder="e.g Hassan Eskandari" v-model="nameCard">
                    </div>

                    <div class="flex flex-col">
                        <span>Card Number</span>
                        <input type="text"
                            class=" border lg:w-[500px] w-[300px] h-[50px] border-gray-3000 rounded-[12px] placeholder:p-3 !px-6"
                            placeholder="e.g 1234 5678 9000 0000" v-model="cardNumber" @keyup="cNumbr"
                            @keydown="cardNumberNme($event)">
                    </div>
                </div>
                <!-- ///////////////////////////cv m d ///////////////////////////////// -->

                <div class="w-full  flex justify-center items-center gap-2  lg:gap-3  lg:flex-row ">
                    <div class="flex flex-col gap-2 relative">
                        <span class=" lg:flex">EXP.DATE (MM/YY)</span>

                        <div class="flex gap-2">
                            <input type="number"
                                class=" border w-[70px] lg:w-[80px] lg:h-[40px] h-[50px] border-gray-300 rounded-[8px] placeholder:p-2 !px-4"
                                placeholder="MM" v-model="MM">
                            <input type="number"
                                class=" border w-[70px] lg:w-[80px] lg:h-[40px] h-[50px] border-gray-300 rounded-[8px] placeholder:p-2 !px-4"
                                placeholder="YY" v-model="YY">
                        </div>
                    </div>


                    <div class="flex flex-col gap-2 relative">
                        <span class="lg:flex">CVC</span>
                        <input type="number"
                            class=" border w-[140px] lg:w-[320px] lg:h-[40px] h-[50px] border-gray-300 rounded-[12px] placeholder:p-3 !px-4"
                            placeholder="e.g 123" v-model="cvCard">
                    </div>
                </div>

                <button class="w-[310px] lg:w-[500px] h-[60px] bg-purple-950 rounded-[20px] text-white">Confrim</button>
            </div>
        </section>
    </main>
</template>





<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

input[type="number"] {
    -moz-appearance: textfield;
}
</style>
