<template>
    <div class="navbar-box" id="navbar-pc">
        <div class="container">
            <b-navbar toggleable="lg" type="dark">
                <b-navbar-toggle target="navbar-toggle-collapse" @click="showIcons = !showIcons">
                    <template>
                        <img v-if="!showIcons" src="~/assets/images/icons/close-icon.svg" alt="nav icon" />
                        <img v-else src="~/assets/images/icons/burger-menu-icon.svg" alt="nav icon" />
                    </template>
                </b-navbar-toggle>
                <b-navbar-brand :to="{ name: 'index' }">
                    <img src="~/assets/images/butterfly.svg" class="logo-pc" alt="brand logo"/>
                    <img src="~/assets/images/logo.png" class="logo-mobile" alt="brand logo"/>
                </b-navbar-brand>
                <div class="col pl-0">
                    <div class="nav-top">
                        <img src="~/assets/images/logo-name.svg" alt="logo name"/>
                        <b-navbar-nav class="ml-auto icons" :class="{ hide: !showIcons }">
                            <b-nav-item to="/account/wish-list"><img src="../assets/images/icons/heart.svg" alt="heart"/>
                            </b-nav-item>
                            <b-nav-item @click="$emit('showBasket')">
                                <img src="../assets/images/icons/basket.svg" alt="basket"/>
                                <span class="products-count" v-if="productCount > 0">+{{ productCount }}</span>
                            </b-nav-item>
                            <b-nav-item
                                @click="
                            !$store.state.user.user ? $emit('showRegModal') : $router.push({ name: 'account' })
                        "
                            ><img src="../assets/images/icons/account.svg" alt="account"
                            /></b-nav-item>
                        </b-navbar-nav>
                    </div>
                    <div class="nav-bottom">
                        <b-collapse id="navbar-toggle-collapse" is-nav>
                            <b-navbar-nav class="links">
                                <b-nav-item to="/catalog?isNew=true">New Collection <img class="star"
                                                                                                   src="../assets/images/icons/star.png" alt="star"/>
                                </b-nav-item>
                                <!-- <b-nav-item to="/catalog/ladies">Women’s dancewear</b-nav-item>
                                <b-nav-item to="/catalog/mens">Men’s dancewear</b-nav-item>
                                <b-nav-item to="/catalog/kids">Kid's dancewear</b-nav-item>
                                <b-nav-item to="/catalog/accessories">Dance Accessories</b-nav-item>
                                <b-nav-item to="/catalog/dance_shoes">Dance shoes</b-nav-item>
                                <b-nav-item to="/catalog/performance_costumes">Performance Costumes</b-nav-item> -->
                                <b-nav-item to="/catalog/ladies">Women</b-nav-item>
                                <b-nav-item to="/catalog/mens">Men</b-nav-item>
                                <b-nav-item to="/catalog/kids_dancewear">Kids</b-nav-item>
                                <b-nav-item to="/catalog/accessories">Accessories</b-nav-item>
                                <b-nav-item to="/catalog/dance_shoes">Shoes</b-nav-item>
                                <b-nav-item to="/catalog/performance_costumes">Costumes</b-nav-item>
                                <b-nav-item to="/about-us/">About us</b-nav-item>
                                <b-nav-item to="/contacts/">Contact us</b-nav-item>
                            </b-navbar-nav>
                        </b-collapse>
                    </div>
                </div>
            </b-navbar>
            <div class="col-auto nav-caption">
                <div>
                    <img src="../assets/images/icons/truck_white.svg" alt="truck icon"/>
                    Free shipping within UAE.
                </div>
                <div>
                    <img src="../assets/images/icons/return.svg" alt="return icon"/>
                    Full refund & return.
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'TheNavbarPC',
        data() {
            return {
                showIcons: true,
            };
        },
        computed: {
            user() {
                return this.$store.state.user.user;
            },
            productCount() {
                return this.$store.state.product.itemsCount;
            },
        },
        created() {
            this.$store.commit('product/update_items_count');
        },
    };
</script>
<style lang="less">
    #navbar-pc {
        .navbar-toggle-collapse {
            flex-flow: column;
        }

        .nav-top {
            display: flex;
            justify-content: space-between;
            align-items: center;

            img {
                display: block;

                @media @large {
                    display: none;
                }
            }
        }

        .nav-bottom {
            .navbar-nav {
                display: flex;
                justify-content: space-between;
                width: 100%;
                padding-top: 10px;
            }
        }

        .navbar {
            padding: 0px;
            justify-content: left;

            .navbar-brand {

                .logo-mobile {
                    display: none;
                    @media @large {
                        display: block;
                        width: 100px;
                    }
                }

                .logo-pc {
                    height: 120px;
                    width: auto;
                    @media @large {
                        display: none;
                    }
                }
            }

            .navbar-toggler {
                border: none !important;
                padding: 0;
                box-shadow: none !important;
                margin-right: 15px;
            }

            .icons {
                .products-count {
                    position: absolute;
                    color: @yellow;
                    font-size: 14px;
                    top: -17px;
                    left: 11px;
                    white-space: nowrap;
                }

                .nav-item {
                    &:not(:last-child) {
                        margin-right: 15px;
                    }

                    .nav-link {
                        position: relative;
                        padding: 0px;
                    }
                }

                @media @large {
                    position: absolute;
                    right: 0px;
                    top: 32px;
                    flex-direction: row;
                }
            }

            .links {
                @media @large {
                    padding-bottom: 100px;
                }

                .nav-item {
                    &:not(:last-child) {
                        //margin-right: 30px;
                    }

                    @media (max-width: 1200px) {
                        &:not(:last-child) {
                            //margin-right: 15px;
                        }
                    }

                    @media @large {
                        &:not(:last-child) {
                            margin-right: 0;
                        }
                    }

                    .nav-link {
                        display: flex;
                        align-items: center;
                        font-family: 'Inter-Light';
                        font-size: 14px;
                        line-height: 17px;
                        padding: 0px;
                        text-transform: uppercase;
                        color: @white !important;

                        @media @large {
                            margin-top: 30px;
                            justify-content: center;
                        }

                        @media @extraLarge {
                            font-size: 12px;
                        }

                        img {
                            margin-left: 10px;
                        }
                    }
                }
            }
        }
        .nav-caption {
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 14px;
            color: #fff;
            padding-bottom: 7px;
            
            div:nth-child(2) img {margin-left: 10px;}
            img {
                margin-right: 10px;
            }
        }
    }
</style>
<style lang="less" scoped>
    .hide {
        display: none;
    }

    .navbar-box {
        background: @black;
    }
</style>
