<template>
    <footer>
        <div class="container">
            <div class="row" style="color:white;">
                <div class="col-md-3 logo">
                    <a href=""><img src="../assets/logo.png" width=100 alt="logo image"></a>
                    <ul style="list-style:none;line-height: 2;">
                        <li>Địa chỉ: An Khánh, Ninh Kiều, Cần Thơ.</li>

                        <li><i class="fa fa-phone"> </i> 0369818290 </li>


                        <li><i class="fa fa-envelope"> </i> khanhb1305@gmail.com</li>

                    </ul>
                </div>
                <div class="col-md-2">
                    DANH MỤC SẢN PHẨM

                    <ul>
                        <li>Tất cả sản phẩm</li>
                        <li>Set quà tặng</li>
                        <li>Gấu bông và gối</li>
                        <li>Balo và túi</li>
                    </ul>

                </div>
                <div class="col-md-2 ">
                    LIÊN HỆ VỚI CHÚNG TÔI

                    <ul>
                        <li>Giờ mở cửa: <br>T2 - CN: 9h00 - 21h00</li>
                        <li>Xem bản đồ</li>
                        <li>Tài khoản</li>
                    </ul>

                </div>
                <div class="col-md-2 ">
                    CHÍNH SÁCH BÁN HÀNG

                    <ul>
                        <li>Giới thiệu</li>
                        <li>Chính sách đổi trả</li>
                        <li>Phương thức thanh toán</li>
                        <li>Phương thức vận chuyển</li>
                        <li>Chính sách bảo mật</li>
                    </ul>

                </div>
                <div class="col-md-2 text-center">
                    <p>CHỨNG NHẬN</p>
                    <div>
                        <img src="../assets/fot_chung_nhan.png" width=150 alt="image" />
                    </div>
                    <br>
                    <div>
                        <img src="../assets/fot_chung_nhan2.png" width=150 alt="image" />
                    </div>
                </div>
            </div>
        </div>

    </footer>
    <div class="footer-bottom">
        Copyright &copy; 2023 Turtle-K. All Rights Reserved.
        {{ selectedValue }}
    </div>

</template>
<script>
export default {
    name: 'Footer_custom',
    props:['selectedValue']
}
</script>
    
<style scoped>
footer {
    background-color: pink;
    color: white;
    font-weight: bold;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.footer-bottom {
    margin-top: 1px;
    background-color: pink;
    color: white;
    padding: 10px 0;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>