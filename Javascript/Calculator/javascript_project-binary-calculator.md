---
title: Binary Calculator
layout: post
permalink: /javascript/project/binary-calculator
---



{% assign BITS = 8 %}

<style>
    td {
        text-align: center;
        vertical-align: middle;
    }

    .my-button {
    background-color: #00b400; /* Button background color */
    color: black;              /* Text color */
    border: none;              /* Remove default border */
    padding: 10px 20px;        /* Padding inside the button */
    border-radius: 5px;        /* Rounded corners */
    font-size: 16px;           /* Font size */
    cursor: pointer;           /* Change cursor on hover */
    transition: background-color 0.3s, transform 0.2s; /* Smooth transitions */
    }

    .my-button:hover {
    background-color: #018c10; /* Change background color on hover */
    transform: scale(1.05);    /* Slightly enlarge button on hover */
    }

    .my-button:active {
    background-color: #006400; /* Change background color when button is pressed */
    transform: scale(0.95);    /* Slightly shrink button when pressed */
    }

    .my-table {
        background-color: #bdffbd;
        color: black
    }
</style>

<table>
    <thead>
        <tr class="header" id="table">
            <th class="my-table">Plus</th>
            <th class="my-table">Binary</th>
            <th class="my-table">Octal</th>
            <th class="my-table">Hexadecimal</th>
            <th class="my-table">Decimal</th>
            <th class="my-table">Minus</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="my-table"><button class="my-button"><div class="calc-button" id="add1" onclick="add(1)">+1</div></button></td>
            <td class="my-table" id="binary">00000000</td>
            <td class="my-table" id="octal">0</td>
            <td class="my-table" id="hexadecimal">0</td>
            <td class="my-table" id="decimal">0</td>
            <td class="my-table"><button class="my-button"><div class="calc-button" id="sub1" onclick="add(-1)">-1</div></button></td>
        </tr>
    </tbody>
</table>

{% comment %}
Liquid for loop includes last number, thus the Minus
{% endcomment %}
{% assign bits = BITS | minus: 1 %} 

<table>
    <thead>
        <tr>
            {% comment %}
            Build many bits
            {% endcomment %}
            {% for i in (0..bits) %}
            <th><img id="bulb{{ i }}" src="{{site.baseurl}}/images/bulb_off.png" alt="" width="40" height="Auto">
                <div class="button" id="butt{{ i }}" onclick="javascript:toggleBit({{ i }})">Turn on</div>
            </th>
            {% endfor %}
        </tr>
    </thead>
    <tbody>
        <tr>
            {% comment %}
            Value of bit
            {% endcomment %}
            {% for i in (0..bits) %}
            <td><input type='text' id="digit{{ i }}" Value="0" size="1" readonly></td>
            {% endfor %}
        </tr>
    </tbody>
</table>

<script>
    const BITS = {{ BITS }};
    const MAX = 2 ** BITS - 1;
    const MSG_ON = "Turn on";
    const IMAGE_ON = "{{site.baseurl}}/images/bulb_on.gif";
    const MSG_OFF = "Turn off";
    const IMAGE_OFF = "{{site.baseurl}}/images/bulb_off.png"

    // return string with current value of each bit
    function getBits() {
        let bits = "";
        for(let i = 0; i < BITS; i++) {
            bits = bits + document.getElementById('digit' + i).value;
        }
        return bits;
    }
    // setter for Document Object Model (DOM) values
    function setConversions(binary) {
        document.getElementById('binary').innerHTML = binary;
        // Octal conversion
        document.getElementById('octal').innerHTML = parseInt(binary, 2).toString(8);
        // Hexadecimal conversion
        document.getElementById('hexadecimal').innerHTML = parseInt(binary, 2).toString(16);
        // Decimal conversion
        document.getElementById('decimal').innerHTML = parseInt(binary, 2).toString();
    }
    // convert decimal to base 2 using modulo with divide method
    function decimal_2_base(decimal, base) {
        let conversion = "";
        // loop to convert to base
        do {
            let digit = decimal % base;           // obtain right most digit
            conversion = "" + digit + conversion; // what does this do? inserts digit to front of string
            decimal = ~~(decimal / base);         // what does this do? divides by base what is ~~? force whole number
        } while (decimal > 0);                    // why while at the end? 0 pads front of binary number
            // loop to pad with zeros
            if (base === 2) {                     // only pad for binary conversions
                for (let i = 0; conversion.length < BITS; i++) {
                    conversion = "0" + conversion;
            }
        }
        return conversion;
    }
    // toggle selected bit and recalculate
    function toggleBit(i) {
        //alert("Digit action: " + i );
        const dig = document.getElementById('digit' + i);
        const image = document.getElementById('bulb' + i);
        const butt = document.getElementById('butt' + i);
        // Change digit and visual
        if (image.src.match(IMAGE_ON)) {
            dig.value = 0;
            image.src = IMAGE_OFF;
            butt.innerHTML = MSG_ON;
        } else {
            dig.value = 1;
            image.src = IMAGE_ON;
            butt.innerHTML = MSG_OFF;
        }
        // Binary numbers
        const binary = getBits();
        setConversions(binary);
    }
    // add is positive integer, subtract is negative integer
    function add(n) {
        let binary = getBits();
        // convert to decimal and do math
        let decimal = parseInt(binary, 2);
        if (n > 0) {  // PLUS
            decimal = MAX === decimal ? 0 : decimal += n; // OVERFLOW or PLUS
        } else  {     // MINUS
            decimal = 0 === decimal ? MAX : decimal += n; // OVERFLOW or MINUS
        }
        // convert the result back to binary
        binary = decimal_2_base(decimal, 2);
        // update conversions
        setConversions(binary);
        // update bits
        for (let i = 0; i < binary.length; i++) {
            let digit = binary.substr(i, 1);
            document.getElementById('digit' + i).value = digit;
            if (digit === "1") {
                document.getElementById('bulb' + i).src = IMAGE_ON;
                document.getElementById('butt' + i).innerHTML = MSG_OFF;
            } else {
                document.getElementById('bulb' + i).src = IMAGE_OFF;
                document.getElementById('butt' + i).innerHTML = MSG_ON;
            }
        }
    }
</script>
