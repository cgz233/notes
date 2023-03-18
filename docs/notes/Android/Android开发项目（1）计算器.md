# Android开发项目（1）计算器

**更改主题**

AndroidMainfest.xml中`android:theme="@style/Theme.Calculator"`为Android的主题配置，Cltr + B 进入，更改为 `    <style name="Theme.Calculator" parent="Theme.MaterialComponents.DayNight.DarkActionBar.Bridge">`，这样更改按钮颜色才可以显示

**MainActivity.java**

```java
package com.xiaochen.calculator;


import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    private TextView tv_result;
    //第一个操作数
    private String firstNum = "";
    //运算符
    private String operator = "";
    //第二个操作数
    private String secondNum = "";
    //计算结果
    private String result = "";
    //显示的文本内容
    private String showText = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //获取文本
        tv_result = findViewById(R.id.tv_result);
        //给按钮注册点击监听器

        findViewById(R.id.btn_cancel).setOnClickListener(this);
        findViewById(R.id.btn_divide).setOnClickListener(this); // “除法”按钮
        findViewById(R.id.btn_multiply).setOnClickListener(this); // “乘法”按钮
        findViewById(R.id.btn_clear).setOnClickListener(this); // “清除”按钮
        findViewById(R.id.btn_seven).setOnClickListener(this); // 数字7
        findViewById(R.id.btn_eight).setOnClickListener(this); // 数字8
        findViewById(R.id.btn_nine).setOnClickListener(this); // 数字9
        findViewById(R.id.btn_plus).setOnClickListener(this); // “加法”按钮
        findViewById(R.id.btn_four).setOnClickListener(this); // 数字4
        findViewById(R.id.btn_five).setOnClickListener(this); // 数字5
        findViewById(R.id.btn_six).setOnClickListener(this); // 数字6
        findViewById(R.id.btn_minus).setOnClickListener(this); // “减法”按钮
        findViewById(R.id.btn_one).setOnClickListener(this); // 数字1
        findViewById(R.id.btn_two).setOnClickListener(this); // 数字2
        findViewById(R.id.btn_three).setOnClickListener(this); // 数字3
        findViewById(R.id.btn_reciprocal).setOnClickListener(this); // 求倒数按钮
        findViewById(R.id.btn_zero).setOnClickListener(this); // 数字0
        findViewById(R.id.btn_dot).setOnClickListener(this); // “小数点”按钮
        findViewById(R.id.btn_equal).setOnClickListener(this); // “等号”按钮
        findViewById(R.id.ib_sqrt).setOnClickListener(this); // “开平方”按钮


    }

    @Override
    public void onClick(View v) {
        String inputText = "";
        if (v.getId() == R.id.ib_sqrt) {
            inputText = "√";
        } else if(v.getId() == R.id.btn_dot){
            if (firstNum.equals("") || secondNum.equals("")){
                inputText = "0.";
            }
        }else {
            inputText = ((TextView) v).getText().toString();

        }

        switch (v.getId()) {
            //清楚按钮
            case R.id.btn_clear:
                clear();
                break;
            //点击了取消按钮
            case R.id.btn_cancel:
                if(firstNum.equals("")){
                    return;
                }
                //    str = str.substring(0, str.length() - 1);
                showText = showText.substring(0, showText.length() - 1);
                if (operator.equals("")) {
                    firstNum = firstNum.substring(0,firstNum.length()-1);
                }else if (!operator.equals("") && secondNum.equals("")){
                    operator = "";
                }else {
                    secondNum = secondNum.substring(0,secondNum.length()-1);
                }
                refreshText(showText);
                break;
            //点击了加减乘除
            case R.id.btn_plus:
            case R.id.btn_minus:
            case R.id.btn_multiply:
            case R.id.btn_divide:
                if (!operator.equals("")){
                    clear();
                    refreshText("还没开发多个运算符运算呢");

                    return;
                }
                operator = inputText;
                refreshText(showText + operator);

                break;
            //=
            case R.id.btn_equal:
                if (firstNum.equals("181013") || firstNum.equals("20181013")){//彩蛋
                    clear();
                    refreshText("第一天");
                    return;
                }

                if (firstNum.equals("") || secondNum.equals("") || operator.equals("")){
                    return;
                }
                double calculate_result = calculateFour();
                refreshOperate(String.valueOf(calculate_result));
                refreshText(showText + "=" + result);
                break;
            //开根号
            case R.id.ib_sqrt:
                if (!operator.equals("")){
                    clear();
                    refreshText("先算完前面的哦");

                    return;
                }
                double sqrt_result = Math.sqrt(Double.parseDouble(firstNum));
                refreshOperate(String.valueOf(sqrt_result));
                refreshText(showText + "√=" + result);
                break;
            //求倒数
            case R.id.btn_reciprocal:
                if (!operator.equals("")){
                    clear();
                    refreshText("先算完前面的哦");
                    return;
                }
                double reciprocal_result = 1.0/Double.parseDouble(firstNum);
                refreshOperate(String.valueOf(reciprocal_result));
                refreshText(showText + "/=" + result);
                break;
            default:
                if (result.length() > 0 && operator.equals("") || showText.equals("第一天")
                        || showText.equals("先算完前面的哦") || showText.equals("还没开发多个运算符运算呢")){
                    clear();
                }
                if (operator.equals("")) {
                    firstNum = firstNum + inputText;
                } else {
                    secondNum = secondNum + inputText;
                }
                if (showText.equals("0") && !inputText.equals(".")) {
                    refreshText(inputText);
                } else {
                    refreshText(showText + inputText);
                }
                break;
        }

    }

    private double calculateFour() {
        switch (operator){
            case "＋":
                return Double.parseDouble(firstNum) + Double.parseDouble(secondNum);
            case "－":
                return Double.parseDouble(firstNum) - Double.parseDouble(secondNum);
            case "×":
                return Double.parseDouble(firstNum) * Double.parseDouble(secondNum);
            default:
                return Double.parseDouble(firstNum) / Double.parseDouble(secondNum);
        }
    }

    //清空并初始化
    private void clear() {
        refreshOperate("");
        refreshText("");
    }

    private void refreshOperate(String new_result){
        result = new_result;
        firstNum = result;
        secondNum = "";
        operator = "";
    }

    private void refreshText(String text) {
        showText = text;
        tv_result.setText(showText);
    }
}
```

**activity_main.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#EEEEEE"
    android:orientation="vertical"
    android:padding="5dp">

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">


            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:text="Android开发学习项目(一)"
                android:textColor="@color/black"
                android:textSize="20sp" />

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:text="@string/simple_calculator"
                android:textColor="@color/black"
                android:textSize="20sp" />

            <TextView
                android:id="@+id/tv_result"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@color/white"
                android:gravity="right|bottom"
                android:lines="3"
                android:text="欢迎使用"
                android:textColor="@color/black"
                android:textSize="25sp" />

            <GridLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:columnCount="4"
                android:rowCount="5">

                <Button
                    android:id="@+id/btn_cancel"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/cancel"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_divide"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/divide"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_multiply"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/multiply"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_clear"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/clear"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_seven"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/seven"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_eight"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/eight"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_nine"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/nine"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_plus"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/plus"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_four"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/four"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_five"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/five"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_six"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/six"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_minus"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/minus"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_one"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/one"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_two"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/two"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_three"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/three"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <ImageButton
                    android:id="@+id/ib_sqrt"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:scaleType="centerInside"
                    android:src="@drawable/sqrt" />

                <Button
                    android:id="@+id/btn_reciprocal"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/reciprocal"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_zero"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/zero"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_dot"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/dot"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

                <Button
                    android:id="@+id/btn_equal"
                    android:layout_width="0dp"
                    android:layout_height="@dimen/button_height"
                    android:layout_columnWeight="1"
                    android:gravity="center"
                    android:text="@string/equal"
                    android:textColor="@color/black"
                    android:textSize="@dimen/button_font_size" />

            </GridLayout>

                        <ImageView
                            android:id="@+id/iv_scale"
                            android:layout_width="match_parent"
                            android:layout_height="400dp"
                            android:layout_marginTop="5dp"
                            android:src="@drawable/xiaoxin"
                            android:scaleType="centerCrop"/>


        </LinearLayout>



    </ScrollView>

</LinearLayout>
```

**dimens.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <dimen name="button_font_size">30sp</dimen>
    <dimen name="button_height">75dp</dimen>

</resources>
```

**strings.xml**

```xml
<resources>
    <string name="app_name">小陈的计算器</string>
    <string name="hello">小陈安卓开发</string>
    <string name="simple_calculator">小陈の计算器</string>
    <string name="cancel">CE</string>
    <string name="divide">÷</string>
    <string name="multiply">×</string>
    <string name="clear">C</string>
    <string name="seven">7</string>
    <string name="eight">8</string>
    <string name="nine">9</string>
    <string name="plus">＋</string>
    <string name="four">4</string>
    <string name="five">5</string>
    <string name="six">6</string>
    <string name="minus">－</string>
    <string name="one">1</string>
    <string name="two">2</string>
    <string name="three">3</string>
    <string name="reciprocal">1/x</string>
    <string name="zero">0</string>
    <string name="dot">.</string>
    <string name="equal">＝</string>
</resources>
```