Мартиросян Артём
Вариант №12

<img src = "image/1.png"></img>
<img src = "image/2.png"></img>

```Kt
package com.example.ekz

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.compose.ui.tooling.preview.Preview
import java.math.BigInteger

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme {
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    FactorialScreen()
                }
            }
        }
    }
}

@Composable
fun FactorialScreen() {
    var inputText by remember { mutableStateOf("") }
    var resultText by remember { mutableStateOf("") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(20.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        OutlinedTextField(
            value = inputText,
            onValueChange = { inputText = it },
            label = { Text("Введите число N") },
            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(16.dp))

        Button(
            onClick = {
                val n = inputText.toIntOrNull()
                if (n != null && n >= 0) {
                    var res = BigInteger.ONE
                    for (i in 1..n) {
                        res = res.multiply(BigInteger.valueOf(i.toLong()))
                    }
                    resultText = "Результат $n! = $res"
                } else {
                    resultText = "Введите целое число >= 0"
                }
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Посчитать факториал")
        }

        Spacer(modifier = Modifier.height(24.dp))

        Text(
            text = resultText,
            fontSize = 20.sp
        )
    }
}

@Preview(showBackground = true)
@Composable
fun FactorialScreenPreview() {
    MaterialTheme {
        FactorialScreen()
    }
}
```
