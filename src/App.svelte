<script>

    let package_price = localStorage.getItem("package_price") || 26 // стоимость пака факторки
    let package_amount = localStorage.getItem("package_amount") || 12  // число паков для сдачи
    let onyxArcheumEssence_recived = localStorage.getItem("onyxArcheumEssence_recived") || 27 // кол-во раствора получаемого при сдаче пака
    let onyxArcheumEssence_auctionPrice = localStorage.getItem("onyxArcheumEssence_auctionPrice") || 2.4 // стоимость раствора на аукционе
    let or_buy = localStorage.getItem("or_buy") || 45 // ОР на покупку пака
    let or_sell = localStorage.getItem("or_sell") || 105 // ОР на сдачу пака

    $: package_income = Number(onyxArcheumEssence_recived) * Number(onyxArcheumEssence_auctionPrice)
    $: package_profit = package_income - Number(package_price)
    $: gold_required_for_purchase = Number(package_amount) * Number(package_price)
    $: profit_totala = (package_income - Number(package_price)) * Number(package_amount)
    $: or_per_package = Number(or_buy) + Number(or_sell)
    $: or_total = or_per_package * Number(package_amount)

    function handle__package_price__on_input(event) {
        console.log(localStorage.getItem("package_price"))
        package_price = event.target.value
    }

    function handle__package_amount__on_input(event) {
        localStorage.setItem("package_amount", event.target.value)
        package_amount = event.target.value
    }

    function handle__onyxArcheumEssence_recived__on_input(event) {
        localStorage.setItem("onyxArcheumEssence_recived", event.target.value)
        onyxArcheumEssence_recived = event.target.value
    }

    function handle__onyxArcheumEssence_auctionPrice__on_input(event) {
        localStorage.setItem("onyxArcheumEssence_auctionPrice", event.target.value)
        onyxArcheumEssence_auctionPrice = event.target.value
    }

    function handle__or_buy__on_input(event) {
        localStorage.setItem("or_buy", event.target.value)
        or_buy = event.target.value
    }

    function handle__or_sell__on_input(event) {
        localStorage.setItem("or_sell", event.target.value)
        or_sell = event.target.value
    }

</script>

<header>
    <h1>Факторкулятор</h1>
    <h2>Калькулятор стоимости<br/>факторных паков</h2>
</header>

<section class="content">

    <section class="values">
    
        <div class="block">
            <label for="package_price">Цена пака на фактории</label>
            <input id="package_price" type="number" value={package_price} on:input={handle__package_price__on_input} >
        </div>

        <div class="block">
            <label for="package_amount">Количество паков</label>
            <input id="package_amount" type="number" value={package_amount} on:input={handle__package_amount__on_input} >
        </div>

        <div class="block">
            <label for="onyxArcheumEssence_recived">Получено раствора за пак</label>
            <input id="onyxArcheumEssence_recived" type="number" value={onyxArcheumEssence_recived} on:input={handle__onyxArcheumEssence_recived__on_input} >
        </div>

        <div class="block">
            <label for="onyxArcheumEssence_auctionPrice">Цена раствора на аукционе</label>
            <input id="onyxArcheumEssence_auctionPrice" type="number" value={onyxArcheumEssence_auctionPrice} on:input={handle__onyxArcheumEssence_auctionPrice__on_input} >
        </div>

        <div class="block">
            <label for="or_buy">ОР на покупку пака</label>
            <input id="or_buy" type="number" value={or_buy} on:input={handle__or_buy__on_input} >
        </div>

        <div class="block">
            <label for="or_sell">ОР на сдачу пака</label>
            <input id="or_sell" type="number" value={or_sell} on:input={handle__or_sell__on_input} >
        </div>

    </section>
  
    <section class="result">
        
        <div class="block">

            <h1>Результат</h1>

            <div class="result_line">
                <div class="title">Цена паков:</div>
                <div class="price">{(gold_required_for_purchase).toFixed(2)}</div>
            </div>

            <div class="result_line">
                <div class="title">Прибыль с пака:</div>
                <div class="price">{(package_profit).toFixed(2)}</div>
            </div>
            
            <div class="result_line">
                <div class="title">Прибыль:</div>
                <div class="price">{(profit_totala).toFixed(2)}</div>
            </div>
            
            <div class="result_line">
                <div class="title">Затрата ОР на пак:</div>
                <div class="price">{(or_per_package).toFixed(0)}</div>
            </div>

            <div class="result_line">
                <div class="title">Затрата ОР всего:</div>
                <div class="price">{(or_total).toFixed(0)}</div>
            </div>

        </div>

    </section>

</section>