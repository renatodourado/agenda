let app = new Vue({
    el:'#app',
    data:{
        nomeInput:'',
        emailInput:'',
        foneInput:'',
        showModal:false,   
        modal:false,   
        selected:null,     
        nomePronto:false,
        lista:[
            //{nome: this.nomeInput, email: this.emailInput, fone: this.foneInput},            
           {nomeInput: this.nomeInput, emailInput: this.emailInput, foneInput: this.foneInput},
            
        ],
        timer:null
      },
    watch:{
        nomeInput:function(){
            if(this.timer !=null){
                clearTimeout(this.timer);
            }
            if(this.nomeInput != ''){                 
                this.nomePronto = false;
                this.timer = setTimeout(this.ficarPronto,1000);
            }
        }
    },
    methods:{
        ficarPronto:function(){           
            if(this.nomeInput.length > 2){
                this.nomePronto = true;
            }
        },
            
        add: function(){
            this.lista.push({
                nomeInput: this.nomeInput,
            })
            this.nomeInput = '';
            this.nomePronto = false;

            this.lista.push({
                emailInput: this.emailInput,
            });
            this.emailInput = '';
            this.nomePronto = false;

            this.lista.push({
                foneInput: this.foneInput,
            });
            this.foneInput = '';
            this.nomePronto = false;   
            this.add ++        
        },

        remove:function(){
            this.lista.splice(this.selected, 1);
            this.showModal = false;
        },

        toggleModal:function(index){
            this.showModal = !this.showModal;

            if(index !== undefined){
                this.selected = index;
            }
           
        }

       
    }

    // computed:{
    //     totalTexto:function(){
    //         return " Números de contato na agenda: " + this.lista.length;
    //     }
    // }

});


