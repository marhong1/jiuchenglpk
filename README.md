<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>礼品卡购买平台</title>
    <style>
        body { font-family: "微软雅黑", Arial; margin: 0; background: #f5f5f5; }
        .container { width: 98%; max-width: 800px; margin: 40px auto; background: #fff; border-radius: 12px; padding: 24px; box-shadow: 0 3px 16px #ddd;}
        h1 { color: #368; font-size: 2.2em;}
        .card-list { display: flex; gap: 24px; flex-wrap: wrap; margin: 30px 0;}
        .gift-card { flex: 1 1 230px; background: #f2f7fb; border-radius: 8px; padding: 18px 16px; min-width: 200px;}
        .gift-card h3 { margin: 0 0 12px 0; }
        .gift-card p { margin: 0 0 10px 0; }
        form { margin-top: 30px; }
        label { display: block; margin-top: 12px; font-weight: bold; }
        input, select { padding: 7px; border-radius: 4px; border: 1px solid #bbb; width: 100%; margin-top: 4px;}
        .pay-ways img { width: 100px; margin-right: 16px; }
        .pay-ways span { display: block; margin-bottom: 10px;}
        button { margin-top: 24px; padding: 10px 32px; background: #368; color: #fff; border: none; border-radius: 6px; font-size: 1.1em;}
        #success-msg { color: green; font-weight: bold; margin-top: 18px; display:none;}
    </style>
</head>
<body>
<div class="container">
    <h1>欢迎来到礼品卡购买平台</h1>
    <p>支持微信、支付宝、USDT支付。请选择您需要的礼品卡，填写信息并上传支付凭证，管理员将在核实后为您发卡。</p>
    <div class="card-list">
        <div class="gift-card">
            <h3>京东E卡</h3>
            <p>面额：¥100</p>
            <p>售价：¥102</p>
        </div>
        <div class="gift-card">
            <h3>天猫超市卡</h3>
            <p>面额：¥200</p>
            <p>售价：¥204</p>
        </div>
        <div class="gift-card">
            <h3>Steam充值卡</h3>
            <p>面额：¥50</p>
            <p>售价：¥51</p>
        </div>
    </div>
    <form id="order-form">
        <label>选择礼品卡
            <select name="card-type" required>
                <option value="">请选择</option>
                <option value="京东E卡-100">京东E卡 ¥100</option>
                <option value="天猫超市卡-200">天猫超市卡 ¥200</option>
                <option value="Steam-50">Steam充值卡 ¥50</option>
            </select>
        </label>
        <label>购买数量
            <input type="number" name="quantity" min="1" max="10" value="1" required>
        </label>
        <label>联系方式（邮箱或微信号）
            <input type="text" name="contact" placeholder="输入您的邮箱或微信号" required>
        </label>
        <label>选择支付方式
            <select name="pay-way" id="pay-way" required>
                <option value="">请选择</option>
                <option value="wechat">微信支付</option>
                <option value="alipay">支付宝</option>
                <option value="usdt">USDT支付</option>
            </select>
        </label>
        <div class="pay-ways" id="pay-qrcodes" style="margin-top:14px; display:none;">
            <span>请使用下方二维码/地址完成支付，然后上传截图：</span>
            <div id="qrcode-wechat" style="display:none;">
                <img src="https://your-wechat-qrcode-url.png" alt="微信支付二维码"><br>微信收款码
            </div>
            <div id="qrcode-alipay" style="display:none;">
                <img src="https://your-alipay-qrcode-url.png" alt="支付宝二维码"><br>支付宝收款码
            </div>
            <div id="qrcode-usdt" style="display:none;">
                <img src="https://your-usdt-qrcode-url.png" alt="USDT收款码"><br>USDT地址：<b>TRC20-xxxxxxxxxxxxxx</b>
            </div>
        </div>
        <label>上传支付截图/哈希
            <input type="file" name="pay-proof" accept="image/*">
            <input type="text" name="usdt-hash" placeholder="如为USDT支付，请填写区块哈希">
        </label>
        <button type="submit">提交订单</button>
        <div id="success-msg">订单已提交，请等待审核！</div>
    </form>
</div>
<script>
    // 支付方式切换二维码
    document.getElementById('pay-way').addEventListener('change', function() {
        document.getElementById('pay-qrcodes').style.display = 'block';
        document.getElementById('qrcode-wechat').style.display = 'none';
        document.getElementById('qrcode-alipay').style.display = 'none';
        document.getElementById('qrcode-usdt').style.display = 'none';
        if (this.value === 'wechat') {
            document.getElementById('qrcode-wechat').style.display = 'block';
        } else if (this.value === 'alipay') {
            document.getElementById('qrcode-alipay').style.display = 'block';
        } else if (this.value === 'usdt') {
            document.getElementById('qrcode-usdt').style.display = 'block';
        }
    });
    // 表单模拟提交
    document.getElementById('order-form').addEventListener('submit', function(e) {
        e.preventDefault();
        document.getElementById('success-msg').style.display = 'block';
        setTimeout(()=>{document.getElementById('success-msg').style.display = 'none';}, 3500);
        this.reset();
        document.getElementById('pay-qrcodes').style.display = 'none';
    });
</script>
</body>
</html>
