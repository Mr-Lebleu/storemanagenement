<template>
<div>
    <div class="d-flex flex-column-fluid">
        <!--begin::Container-->
        <div class="container-fluid">
            <div class="row">
                <div class="col-12">
                    <div class="row">
                        <div class="col-lg-12 col-xl-12">
                            <div class="card card-custom gutter-b bg-transparent shadow-none border-0">
                                <div class="card-header align-items-center  border-bottom-dark px-0">
                                    <div class="card-title mb-0">
                                        <h3 class="card-label mb-0 font-weight-bold text-body">
                                            Sale List
                                        </h3>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-12 ">
                            <div class="card card-custom gutter-b bg-white border-0">
                                <div class="card-body">
                                    <div>
                                        <div class=" table-responsive" id="printableTable">
                                        
                                            <div id="sale_wrapper" class="dataTables_wrapper no-footer">

                                            <div class="dataTables_length" id="sale_length"><label>Afficher 
                                            <select name="sale_length" aria-controls="sale" class="" v-model="limit" v-on:change="fetchsales()">
                                            <option value="10">10</option>
                                            <option value="25">25</option>
                                            <option value="50">50</option>
                                            <option value="100">100</option>
                                            <option value="200">200</option>
                                            <option value="500">500</option>
                                            <option value="1000">1000</option>
                                            </select> entrées</label></div>

                                            <div id="sale_filter" class="dataTables_filter">
                                                <!-- <label>Search:<input type="search" class="" placeholder="" aria-controls="sale" v-model="searchParameter" @keyup="fetchsales()"></label>
                                                 -->
                                                </div>
                                                <table id="sale" class="display dataTable no-footer" sale="grid">
                                                    <thead class="text-body">
                                                        <tr sale="row">
                                                            <th class="sorting" tabindex="0" aria-controls="sale" rowspan="1" colspan="1" aria-sort="ascending" aria-label="ID: activate to sort column descending" style="width: 31.25px;" @click="sorting('id')" :class="(this.$data.sortType == 'asc' || this.$data.sortType == 'ASC') && this.$data.sortBy == 'id'  ? 'sorting_asc' : (this.$data.sortType == 'desc' || this.$data.sortType == 'DESC') && this.$data.sortBy == 'id' ? 'sorting_desc' : 'sorting'">
                                                                Sale ID
                                                            </th>
                                                            <th class="no-sort sorting_disabled" rowspan="1" colspan="1" aria-label="Action">
                                                               Customer
                                                            </th>
                                                            <th class="no-sort sorting_disabled" rowspan="1" colspan="1" aria-label="Action">
                                                                Sale Date
                                                            </th>
                                                            <th class="no-sort sorting_disabled" rowspan="1" colspan="1" aria-label="Action">
                                                                Warehouse
                                                            </th>
                                                            <th class="no-sort sorting_disabled" rowspan="1" colspan="1" aria-label="Action">
                                                                Description
                                                            </th>
                                                            <th class="sorting" tabindex="0" aria-controls="sale" rowspan="1" colspan="1" aria-sort="ascending" aria-label="ID: activate to sort column descending" style="width: 31.25px;" @click="sorting('payable')" :class="(this.$data.sortType == 'asc' || this.$data.sortType == 'ASC') && this.$data.sortBy == 'payable'  ? 'sorting_asc' : (this.$data.sortType == 'desc' || this.$data.sortType == 'DESC') && this.$data.sortBy == 'payable' ? 'sorting_desc' : 'sorting'">
                                                                Total Amount
                                                            </th>
                                                           <th class="sorting" tabindex="0" aria-controls="sale" rowspan="1" colspan="1" aria-sort="ascending" aria-label="ID: activate to sort column descending" style="width: 31.25px;" @click="sorting('amount_paid')" :class="(this.$data.sortType == 'asc' || this.$data.sortType == 'ASC') && this.$data.sortBy == 'amount_paid'  ? 'sorting_asc' : (this.$data.sortType == 'desc' || this.$data.sortType == 'DESC') && this.$data.sortBy == 'amount_paid' ? 'sorting_desc' : 'sorting'">
                                                                Paid Amount
                                                            </th>
                                                            <th class="sorting" tabindex="0" aria-controls="sale" rowspan="1" colspan="1" aria-sort="ascending" aria-label="ID: activate to sort column descending" style="width: 31.25px;" @click="sorting('discount')" :class="(this.$data.sortType == 'asc' || this.$data.sortType == 'ASC') && this.$data.sortBy == 'discount'  ? 'sorting_asc' : (this.$data.sortType == 'desc' || this.$data.sortType == 'DESC') && this.$data.sortBy == 'discount' ? 'sorting_desc' : 'sorting'">
                                                                Discount
                                                            </th>
                                                            <th class="sorting" tabindex="0" aria-controls="sale" rowspan="1" colspan="1" aria-sort="ascending" aria-label="ID: activate to sort column descending" style="width: 31.25px;" @click="sorting('due_amount')" :class="(this.$data.sortType == 'asc' || this.$data.sortType == 'ASC') && this.$data.sortBy == 'due_amount'  ? 'sorting_asc' : (this.$data.sortType == 'desc' || this.$data.sortType == 'DESC') && this.$data.sortBy == 'due_amount' ? 'sorting_desc' : 'sorting'">
                                                                Due Amount
                                                            </th>
                                                            <th class="sorting" tabindex="0" aria-controls="sale" rowspan="1" colspan="1" aria-sort="ascending" aria-label="ID: activate to sort column descending" style="width: 31.25px;" @click="sorting('due_amount')" :class="(this.$data.sortType == 'asc' || this.$data.sortType == 'ASC') && this.$data.sortBy == 'due_amount'  ? 'sorting_asc' : (this.$data.sortType == 'desc' || this.$data.sortType == 'DESC') && this.$data.sortBy == 'due_amount' ? 'sorting_desc' : 'sorting'">
                                                                View
                                                            </th>
                                                        </tr>
                                                    </thead>
                                                    <tbody class="kt-table-tbody text-dark">
                                                        <tr class="kt-table-row kt-table-row-level-0 odd" sale="row" v-for="sale in sales" v-bind:key="sale.id">
                                                            <td class="sorting_1">
                                                                <router-link :to="'/admin/sale-detail/'+sale.id">
                                                                    {{ sale.id }}
                                                                </router-link>
                                                            </td>
                                                            <td>
                                                                {{ sale.customer != null ? sale.customer.customer_first_name+' '+sale.customer.customer_last_name :"" }}
                                                            </td>
                                                            <td>
                                                                {{ sale.sale_date }}
                                                            </td>
                                                            <td>
                                                                {{ sale.warehouse != null ? sale.warehouse.warehouse_name :"" }}
                                                            </td>
                                                            <td>
                                                                {{ sale.desc }}
                                                            </td>
                                                            <td>
                                                                {{ sale.payable }}
                                                            </td>
                                                            <td>
                                                                {{ sale.amount_paid }}
                                                            </td>
                                                            <td>
                                                                {{ sale.discount }}
                                                            </td>
                                                            <td>
                                                                {{ sale.due_amount }}
                                                            </td>
                                                            <td >
                                                                <router-link :to="'/admin/sale-detail/'+sale.id">
                                                                    View
                                                                </router-link>
                                                            </td>
                                                        </tr>
                                                    </tbody>
                                                </table>
                                                <ul class="pagination pagination-sm m-0 float-right">
                                                    <li v-bind:class="[{disabled: !pagination.prev_page_url}]"><a class="page-link" href="#" @click="fetchsales(pagination.prev_page_url)">Précédent</a></li>

                                                    <li class="disabled"><a class="page-link text-dark" href="#">Page {{ pagination.current_page }} of {{ pagination.last_page }}</a></li>

                                                    <li v-bind:class="[{disabled: !pagination.next_page_url}]" class="page-item"><a class="page-link" href="#" @click="fetchsales(pagination.next_page_url)">Suivant</a></li>
                                                </ul>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    
</div>
</template>

<script>
import ErrorHandling from "../../ErrorHandling";
export default {
    data() {
        return {
            display_form: 0,
            sales:[],
            searchParameter: '',
            sortBy: 'id',
            sortType: 'ASC',
            limit: 10,
            error_message: '',
            edit: false,
            actions: false,
            pagination: {},
            request_method: "",
            is_default: "0",
            token: [],
            errors: new ErrorHandling(),
            csrf: document.querySelector('meta[name="csrf-token"]').getAttribute("content")
        };
    },

    methods: {
        fetchsales(page_url) {
            this.$parent.loading = true;
            let vm = this;
            page_url = page_url || "/api/admin/sale";
            var arr = page_url.split('?');
            
            if (arr.length > 1) {
                page_url += '&limit='+this.limit;
            }
            else{
                page_url += '?limit='+this.limit;
            }
            if(this.searchParameter != null){
                page_url += '&searchParameter='+this.searchParameter;
            }
            page_url += '&sortBy='+this.sortBy+'&sortType='+this.sortType;
            page_url +='&getDetail=1&getProduct=1&language_id=1&getProductCombinationDetail=1&language_id=1';

            var responseData = {};

            axios.get(page_url, this.token).then(res => {
                this.sales = res.data.data;
                vm.makePagination(res.data.meta, res.data.links);
            })
            .finally(() => (this.$parent.loading = false));
        },

        makePagination(meta, links) {
            let pagination = {
                current_page: meta.current_page,
                last_page: meta.last_page,
                next_page_url: links.next,
                prev_page_url: links.prev
            };

            this.pagination = pagination;
        },
        sorting(sortBy){
            this.sortBy = sortBy;
            this.sortType = this.sortType == 'asc' || this.sortType == 'ASC' ? this.sortType='desc' : this.sortType = 'asc';
            this.fetchsales();
        },
    },
    mounted() {
     
        var token = localStorage.getItem('token');
        this.token = {
            headers: {
                Authorization: `Bearer ${token}`
            }
        };
        this.fetchsales();
    },
    props: ['loading'],
};
</script>
