<template>
    <div>
        <div class="px-xl-5 px-lg-4 px-3 py-3 page-body">
            <div class="row mb-3">
                <div class="col-sm-12">
                    <div class="d-flex align-items-center justify-content-between flex-wrap">
                        <h3 class="fw-bold mb-0">Điền thông tin đặt phòng</h3>
                    </div>
                </div>
            </div>

            <div class="body-page">
                <div class="card col-sm-12">
                    <div class="d-flex  align-items-center justify-content-between flex-wrap">
                        <h4 class="fw-bold mb-0">Thông tin đặt chỗ</h4>
                    </div>
                    <div class="row">
                        <div class="col-md-6 col-lg-4 col-xl-4">
                            <div class="form-group"><label class="form-label text-muted">Check In <span
                                        class="text-danger">*</span></label>
                                <div class="input-group">
                                    <span class="input-group-text">
                                        <i class="fa fa-calendar-plus-o"></i>
                                    </span>
                                    <input type="datetime-local" v-model="invoice.checkin" name="checkin"
                                        class="form-control">
                                </div>
                            </div>
                        </div>

                        <div class="col-md-6 col-lg-4 col-xl-4">
                            <div class="form-group"><label class="form-label text-muted">Check Out <span
                                        class="text-danger">*</span></label>
                                <div class="input-group">
                                    <span class="input-group-text">
                                        <i class="fa fa-calendar-minus-o"></i>
                                    </span>
                                    <input type="datetime-local" v-model="invoice.checkout" name="checkout"
                                        class="form-control">
                                </div>
                            </div>
                        </div>
                        <div class="col-md-6 col-lg-4 col-xl-4">
                            <div class="form-group"><label class="form-label text-muted">Booking Type</label>
                                <div class="input-group">
                                    <span class="input-group-text"><i class="fa fa-home"></i></span>
                                    <select class="form-select form-control" v-model="selectedBookingType">
                                        <option>Choose Booking Reference</option>
                                        <option v-for="(item, key) in bookingType" :key="key" :value="item.value"
                                            >{{
                                                item.title }}</option>

                                    </select>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="card col-sm-12">
                    <h4>Chọn phòng</h4>
                    <div class="row">
                        <div class=" col-md-2 d-flex" v-for="(item, index) in rooms" :key="index">
                            <input class="hidden" type="checkbox" :name="'room-' + (index + 1)" v-model="item.selected"
                                :disabled="item.disabled" @click.stop />
                            <div class="card w-100"
                                :class="{ 'bg-success': item.selected && !item.disabled, 'bg-primary': !item.selected && !item.disabled, 'bg-danger': item.disabled }"
                                @click="toggleRoom(index)">
                                <div class="p-2">
                                    <h4 class="text-white">{{ item.name }}</h4>
                                    <p class="p-0 text-white"><i class="fa fa-bed mr-2"></i>{{ item.beds }}</p>
                                    <p class="p-0 text-white"><i class="fa fa-eye mr-2"></i>{{ item.view }}</p>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>

                <div class="card col-sm-12">
                    <h4>Thông tin khách hàng</h4>

                    <div class="row">

                        <div class="col-md-6 col-lg-4 col-xl-4">
                            <div class="form-group"><label class="form-label text-muted">Họ & tên Khách Hàng <span
                                        class="text-danger">*</span></label>
                                <div class="input-group">
                                    <span class="input-group-text">
                                        <i class="fa fa-user"></i>
                                    </span>
                                    <input type="input" v-model="invoice.customerName" name="customer_name" required
                                        class="form-control">
                                </div>
                            </div>
                            <div class="form-group"><label class="form-label text-muted">Số điện thoại<span
                                        class="text-danger">*</span></label>
                                <div class="input-group">
                                    <span class="input-group-text">
                                        <i class="fa fa-phone"></i>
                                    </span>
                                    <input type="input" v-model="invoice.customerPhone" name="customer_phone" required
                                        class="form-control">
                                </div>
                            </div>
                            <div class="form-group"><label class="form-label text-muted">Email</label>
                                <div class="input-group">
                                    <span class="input-group-text">
                                        <i class="fa fa-envelope"></i>
                                    </span>
                                    <input type="input" name="customer_email" required class="form-control">
                                </div>
                            </div>
                        </div>

                        <div class="col-md-6 col-lg-8 col-xl-4">
                            <div class="form-group"><label class="form-label text-muted">Ảnh 2 mặt CCCD <span
                                        class="text-danger">*</span></label>
                                <div class="input-group">
                                    <div class="image-uploader">
                                        <!-- Input chọn ảnh -->
                                        <input type="file" multiple accept="image/*" @change="handleMultipleImages" />
                                        <!-- Hiển thị ảnh đã chọn -->
                                        <div v-if="imagePreview && imagePreview.length" class="d-flex">
                                            <div v-for="(src, index) in imagePreview" :key="index" class="preview">
                                                <img :src="src" :alt="'Image ' + index" />
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>


                    </div>

                </div>
                <div class="d-flex">
                    <div class="card col-sm-6">
                        <h4>Khuyến Mãi</h4>
                        <div class="form-group"><label class="form-label text-muted">Chương trình khuyến mãi <span
                                    class="text-danger">*</span></label>
                            <div class="input-group">
                                <span class="input-group-text">
                                    <i class="fa fa-tags"></i>
                                </span>
                                <select name="" id="" v-model="invoice.discount" class="form-control">
                                    <option value="">Chọn chương trình khuyến mãi</option>
                                    <option v-for="(item, index) in discounts" :key="index" :value="item.discount">{{
                                        item.title }}</option>
                                </select>
                            </div>
                        </div>

                    </div>
                    <div class="card col-sm-6">
                        <h4>
                            Hóa đơn tạm
                        </h4>
                        <p>Họ tên khách: {{ invoice.customerName || 'Chưa điền' }}</p>
                        <p>Số điện thoại: {{ invoice.customerPhone || 'Chưa điền' }}</p>
                        <p>Mục đích đặt chỗ: {{ selectedBookingType || 'Chưa chọn' }}</p>
                        <p>Checkin: {{ invoice.checkin || 'Chưa chọn' }}, Checkout: {{ invoice.checkout || 'Chưa chọn'
                            }}</p>
                        <p>Đặt phòng: <span v-if="selectedRooms.length">
                                <span v-for="room in selectedRooms" :key="room.name">
                                    {{ room.name }} ({{ room.price.toLocaleString() }} VNĐ)
                                </span>
                            </span>
                            <span v-else>Chưa chọn phòng</span>
                        </p>
                        <p>Tổng cộng: {{ totalPrice.toLocaleString() }} VNĐ</p>
                        <p>Khuyến mãi: {{ invoice.discount || 'Chưa chọn' }}</p>
                        <p>------------------------------------------------------------------------------------</p>
                        <p>Thành Tiền: {{ finalPrice.toLocaleString() }} VNĐ</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
.preview {
    margin-top: 10px;
    border: 1px solid #ccc;
    padding: 5px;
    display: inline-block;
}

img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
}

.hidden {
    display: none;
    /* Ẩn hoàn toàn phần tử */
}
</style>
<script>
export default {
    data() {
        return {
            imagePreview: null,
            invoice: {
                customerName: '',
                customerPhone: '',
                checkin: '',
                checkout: '',
                discount: null
            },
            selectedBookingType: '',
            rooms: [
                { name: 'Phòng 202', beds: '2 Giường ngủ', view: 'View Biển', price: 1900000, selected: false, disabled: false },
                { name: 'Phòng 203', beds: '1 Giường ngủ', view: 'View Núi', price: 1100000, selected: false, disabled: true },
                { name: 'Phòng 204', beds: '3 Giường ngủ', view: 'View Vườn', price: 4000000, selected: false, disabled: false }
            ],
           
            discounts:
                [
                    {
                        "title": "Ưu đãi đặc biệt mùa đông (20%)",
                        "discount": 20
                    },
                    {
                        "title": "Giảm giá khi đặt phòng trước 30 ngày (15%)",
                        "discount": 15
                    },
                    {
                        "title": "Giảm giá 10% cho khách hàng thành viên (10%)",
                        "discount": 10
                    },
                    {
                        "title": "Khuyến mãi cuối tuần - Ưu đãi cho phòng đôi (25%)",
                        "discount": 25
                    },
                    {
                        "title": "Mùa lễ hội - Tặng thêm 1 đêm miễn phí (50%)",
                        "discount": 50
                    },
                    {
                        "title": "Khuyến mãi gia đình - Giảm giá phòng suite (30%)",
                        "discount": 30
                    },
                    {
                        "title": "Ưu đãi khi đặt từ 3 đêm trở lên (20%)",
                        "discount": 20
                    },
                    {
                        "title": "Ưu đãi 40% cho khách hàng đặt qua ứng dụng (40%)",
                        "discount": 40
                    },
                    {
                        "title": "Ưu đãi đặc biệt cho cặp đôi trong tháng Valentine (35%)",
                        "discount": 35
                    },
                    {
                        "title": "Combo ăn sáng miễn phí và giảm giá phòng (15%)",
                        "discount": 15
                    }
                ]

            ,
            bookingType: [
                {
                    value: 1,
                    title: 'Đặt phòng'
                },
                {
                    value: 2,
                    title: 'Đám cưới'
                },
                {
                    value: 3,
                    title: 'Hoạt động doanh nghiệp'
                },
                {
                    value: 4,
                    title: 'Hội thảo'
                }
            ]
        }
    },
    mounted() {
        console.log(this.rooms);
    },
    computed: {
                selectedRooms() {
                    return this.rooms.filter(room => room.selected);
                },
                totalPrice() {
                    return this.selectedRooms.reduce((total, room) => total + room.price, 0);
                },
                finalPrice() {
                    const discount = this.invoice.discount ? parseFloat(this.invoice.discount) : 0;
                    return this.totalPrice - (this.totalPrice * discount / 100);
                }
            },
    methods: {
        toggleRoom(index) {
            this.rooms[index].selected = !this.rooms[index].selected;
        },
        handleMultipleImages(event) {
            const files = Array.from(event.target.files); // Lấy tất cả các file
            this.imagePreview = files.map(file => URL.createObjectURL(file)); // Tạo mảng các URL
        },
    }
}
</script>