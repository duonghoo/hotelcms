<template>
    <div>
        <div class="px-xl-5 px-lg-4 px-3 py-3 page-body">
            <div class="row mb-3">
                <div class="col-sm-12">
                    <div class="d-flex align-items-center justify-content-between flex-wrap">
                        <h3 class="fw-bold mb-0">Hotels</h3>
                    </div>
                </div>
            </div>
            <ul
                class="row g-2 list-unstyled li_animate row-cols-lg-4 row-cols-md-3 row-cols-sm-2 row-cols-1 row-deck mb-lg-5 mb-4">
                <li class="col" v-for="(item,index) in MenuItems" :key = "index">
                  
                    <router-link :to="item.link" class="card arr_hidden p-4">
                        <i :class="[item.icon, item.color]" class="mb-2"></i>
                        <h6 class="title mb-1 text-dark">{{ item.title }}</h6>
                        <p class="small text-muted mb-0 d-none d-xl-inline-flex"></p>
                        <div class="go-corner">
                            <div class="go-arrow pt-3 pl-2">→</div>
                        </div>
                    </router-link>
                </li>
                
            </ul>
        </div>
    </div>
</template>
<style>
    .card.arr_hidden
    {overflow: hidden;}
    .go-corner {
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.3s ease, visibility 0.3s ease;
    }
    .page-body{
        min-height: 87vh;
    }
    /* Khi hover vào .container, hiển thị go-corner */
    .card:hover .go-corner {
        opacity: 1;
        visibility: visible;
    }
    .card:hover {
        border-color:#354175;

    }

    .li_animate>li:first-child {
    animation-delay: .01s;
    }

    .go-corner {
    background: #354175;
    color: #fff;
    display: flex;
    height: 100%;
   
    position: absolute;
    right:-6px;
    top: 0;
    transform: skew(7deg);
    transition: all .3s ease-out;
    width: 36px;
}

    .go-arrow {
        font-weight: bold;
        font-size: 16px;
    }
</style>
<script>
export default {
    data () 
    {
        return {
            MenuItems : [
                {
                    title: 'Đặt phòng',
                    link: '/admin/room-book',
                    color: 'text-infor',
                    icon : 'fa fa-building'
                },
                
                {
                    title: 'Danh sách phòng',
                    link: '/admin/room-list',
                    color: 'text-infor',
                    icon : 'fa fa-building'
                },
                {
                    title: 'Trạng thái phòng',
                    link: '/admin/room-status',
                    color: 'text-infor',
                    icon : 'fa fa-building'
                },
                {
                    title: 'Tiện ích phòng',
                    link: '/admin/room-facilities',
                    color: 'text-infor',
                    icon : 'fa fa-bathtub'
                },
                {
                    title: 'Dọn phòng',
                    link: '/admin/room-house-keeping',
                    color: 'text-infor',
                    icon : 'fa fa-magic'
                },
                {
                    title: 'Báo cáo đặt phòng',
                    link: '/admin/booking-report',
                    color: 'text-infor',
                    icon : 'fa fa-bed'
                },
                {
                    title: 'Báo cáo thanh toán',
                    link: '/admin/purchase-report',
                    color: 'text-infor',
                    icon : 'fa fa-credit-card-alt'
                },
                {
                    title: 'Chương trình khuyến mãi',
                    link: '/admin/upon',
                    color: 'text-infor',
                    icon : 'fa fa-tags'
                },
                {
                    title: 'Công việc nhân viên',
                    link: '/admin/task',
                    color: 'text-infor',
                    icon : 'fa fa-tasks'
                }
                
            ]
        }
    }
}
</script>