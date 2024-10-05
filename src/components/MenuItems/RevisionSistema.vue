<template>
  <div class="container">
    <form>
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-heart-pulse"></i> Revisión por Sistemas</span
            >
            <span class="opciones-formulario"></span>
          </p>
        </div>

        <div class="card-body">
          <ul class="nav nav-tabs" id="myTab" role="tablist">
            <li class="nav-item" role="presentation">
              <button
                class="nav-link active"
                id="home-tab"
                data-bs-toggle="tab"
                data-bs-target="#home-tab-pane"
                type="button"
                role="tab"
                aria-controls="home-tab-pane"
                aria-selected="true"
              >
                Registro de Hallazgos
              </button>
            </li>
            <li class="nav-item" role="presentation">
              <button
                class="nav-link"
                id="profile-tab"
                data-bs-toggle="tab"
                data-bs-target="#profile-tab-pane"
                type="button"
                role="tab"
                aria-controls="profile-tab-pane"
                aria-selected="false"
              >
                Historial
              </button>
            </li>
          </ul>
          <div class="tab-content" id="myTabContent">
            <div
              class="tab-pane fade show active"
              id="home-tab-pane"
              role="tabpanel"
              aria-labelledby="home-tab"
              tabindex="0"
            >
              <div class="row mt-3">
                <!-- Textarea - S muscular/esqueletico -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-muscular-esqueletico" class="form-label"
                      ><strong>S muscular/esqueletico</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-muscular-esqueletico"
                      v-model="formData.sMuscularEsqueletico"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S nervioso central y periferico -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label
                      for="s-nervioso-central-periferico"
                      class="form-label"
                      ><strong>S nervioso central y periferico</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-nervioso-central-periferico"
                      v-model="formData.sNerviosoCentralPeriferico"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S gastrointestinal -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-gastrointestinal" class="form-label"
                      ><strong>S gastrointestinal</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-gastrointestinal"
                      v-model="formData.sGastrointestinal"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S endocrino -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-endocrino" class="form-label"
                      ><strong>S endocrino</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-endocrino"
                      v-model="formData.sEndocrino"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S respiratorio -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-respiratorio" class="form-label"
                      ><strong>S respiratorio</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-respiratorio"
                      v-model="formData.sRespiratorio"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S reproductor -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-reproductor" class="form-label"
                      ><strong>S reproductor</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-reproductor"
                      v-model="formData.sReproductor"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S sanguineo -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-sanguineo" class="form-label"
                      ><strong>S sanguineo</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-sanguineo"
                      v-model="formData.sSanguineo"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S linfatico -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-linfatico" class="form-label"
                      ><strong>S linfatico</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-linfatico"
                      v-model="formData.sLinfatico"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S cardiovascular -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-cardiovascular" class="form-label"
                      ><strong>S cardiovascular</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-cardiovascular"
                      v-model="formData.sCardiovascular"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S urinario -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-urinario" class="form-label"
                      ><strong>S urinario</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-urinario"
                      v-model="formData.sUrinario"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S osteoarticular -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-osteoarticular" class="form-label"
                      ><strong>S osteoarticular</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-osteoarticular"
                      v-model="formData.sOsteoarticular"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - S digestivo -->
                <div class="col-lg-3 col-md-12">
                  <div class="mb-3">
                    <label for="s-digestivo" class="form-label"
                      ><strong>S digestivo</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="s-digestivo"
                      v-model="formData.sDigestivo"
                    ></textarea>
                  </div>
                </div>
                <!-- Textarea - Observaciones -->
                <div class="col-lg-12 col-md-12">
                  <div class="mb-3">
                    <label for="observaciones" class="form-label"
                      ><strong>Observaciones</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="observaciones"
                      v-model="formData.observaciones"
                    ></textarea>
                  </div>
                </div>
                <!-- Botón para capturar los datos -->
                <div class="mt-3">
                  <button
                    type="button"
                    class="btn btn-custom btn-icon mb-2"
                    @click="capturarDatos"
                  >
                    Guardar
                  </button>
                </div>
              </div>
            </div>
            <div
              class="tab-pane fade"
              id="profile-tab-pane"
              role="tabpanel"
              aria-labelledby="profile-tab"
              tabindex="0"
            >
              <!-- DataTable -->
              <div class="container">
                <div class="row">
                  <div class="col-lg-12">
                    <div class="table-responsive">
                      <table
                        id="miTabla"
                        class="table table-striped table-bordered"
                        style="width: 100%"
                      >
                        <thead>
                          <tr>
                            <th>Name</th>
                            <th>Position</th>
                            <th>Office</th>
                            <th>Age</th>
                            <th>Start date</th>
                            <th>Salary</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr>
                            <td>Tiger Nixon</td>
                            <td>System Architect</td>
                            <td>Edinburgh</td>
                            <td>61</td>
                            <td>2011-04-25</td>
                            <td>$320,800</td>
                          </tr>
                          <tr>
                            <td>Garrett Winters</td>
                            <td>Accountant</td>
                            <td>Tokyo</td>
                            <td>63</td>
                            <td>2011-07-25</td>
                            <td>$170,750</td>
                          </tr>
                          <tr>
                            <td>Ashton Cox</td>
                            <td>Junior Technical Author</td>
                            <td>San Francisco</td>
                            <td>66</td>
                            <td>2009-01-12</td>
                            <td>$86,000</td>
                          </tr>
                          <tr>
                            <td>Cedric Kelly</td>
                            <td>Senior Javascript Developer</td>
                            <td>Edinburgh</td>
                            <td>22</td>
                            <td>2012-03-29</td>
                            <td>$433,060</td>
                          </tr>
                          <tr>
                            <td>Airi Satou</td>
                            <td>Accountant</td>
                            <td>Tokyo</td>
                            <td>33</td>
                            <td>2008-11-28</td>
                            <td>$162,700</td>
                          </tr>
                          <tr>
                            <td>Brielle Williamson</td>
                            <td>Integration Specialist</td>
                            <td>New York</td>
                            <td>61</td>
                            <td>2012-12-02</td>
                            <td>$372,000</td>
                          </tr>
                          <tr>
                            <td>Herrod Chandler</td>
                            <td>Sales Assistant</td>
                            <td>San Francisco</td>
                            <td>59</td>
                            <td>2012-08-06</td>
                            <td>$137,500</td>
                          </tr>
                          <tr>
                            <td>Rhona Davidson</td>
                            <td>Integration Specialist</td>
                            <td>Tokyo</td>
                            <td>55</td>
                            <td>2010-10-14</td>
                            <td>$327,900</td>
                          </tr>
                          <tr>
                            <td>Colleen Hurst</td>
                            <td>Javascript Developer</td>
                            <td>San Francisco</td>
                            <td>39</td>
                            <td>2009-09-15</td>
                            <td>$205,500</td>
                          </tr>
                          <tr>
                            <td>Sonya Frost</td>
                            <td>Software Engineer</td>
                            <td>Edinburgh</td>
                            <td>23</td>
                            <td>2008-12-13</td>
                            <td>$103,600</td>
                          </tr>
                          <tr>
                            <td>Jena Gaines</td>
                            <td>Office Manager</td>
                            <td>London</td>
                            <td>30</td>
                            <td>2008-12-19</td>
                            <td>$90,560</td>
                          </tr>
                          <tr>
                            <td>Quinn Flynn</td>
                            <td>Support Lead</td>
                            <td>Edinburgh</td>
                            <td>22</td>
                            <td>2013-03-03</td>
                            <td>$342,000</td>
                          </tr>
                          <tr>
                            <td>Charde Marshall</td>
                            <td>Regional Director</td>
                            <td>San Francisco</td>
                            <td>36</td>
                            <td>2008-10-16</td>
                            <td>$470,600</td>
                          </tr>
                          <tr>
                            <td>Haley Kennedy</td>
                            <td>Senior Marketing Designer</td>
                            <td>London</td>
                            <td>43</td>
                            <td>2012-12-18</td>
                            <td>$313,500</td>
                          </tr>
                          <tr>
                            <td>Tatyana Fitzpatrick</td>
                            <td>Regional Director</td>
                            <td>London</td>
                            <td>19</td>
                            <td>2010-03-17</td>
                            <td>$385,750</td>
                          </tr>
                          <tr>
                            <td>Michael Silva</td>
                            <td>Marketing Designer</td>
                            <td>London</td>
                            <td>66</td>
                            <td>2012-11-27</td>
                            <td>$198,500</td>
                          </tr>
                          <tr>
                            <td>Paul Byrd</td>
                            <td>Chief Financial Officer (CFO)</td>
                            <td>New York</td>
                            <td>64</td>
                            <td>2010-06-09</td>
                            <td>$725,000</td>
                          </tr>
                          <tr>
                            <td>Gloria Little</td>
                            <td>Systems Administrator</td>
                            <td>New York</td>
                            <td>59</td>
                            <td>2009-04-10</td>
                            <td>$237,500</td>
                          </tr>
                          <tr>
                            <td>Bradley Greer</td>
                            <td>Software Engineer</td>
                            <td>London</td>
                            <td>41</td>
                            <td>2012-10-13</td>
                            <td>$132,000</td>
                          </tr>
                          <tr>
                            <td>Dai Rios</td>
                            <td>Personnel Lead</td>
                            <td>Edinburgh</td>
                            <td>35</td>
                            <td>2012-09-26</td>
                            <td>$217,500</td>
                          </tr>
                          <tr>
                            <td>Jenette Caldwell</td>
                            <td>Development Lead</td>
                            <td>New York</td>
                            <td>30</td>
                            <td>2011-09-03</td>
                            <td>$345,000</td>
                          </tr>
                          <tr>
                            <td>Yuri Berry</td>
                            <td>Chief Marketing Officer (CMO)</td>
                            <td>New York</td>
                            <td>40</td>
                            <td>2009-06-25</td>
                            <td>$675,000</td>
                          </tr>
                          <tr>
                            <td>Caesar Vance</td>
                            <td>Pre-Sales Support</td>
                            <td>New York</td>
                            <td>21</td>
                            <td>2011-12-12</td>
                            <td>$106,450</td>
                          </tr>
                          <tr>
                            <td>Doris Wilder</td>
                            <td>Sales Assistant</td>
                            <td>Sydney</td>
                            <td>23</td>
                            <td>2010-09-20</td>
                            <td>$85,600</td>
                          </tr>
                          <tr>
                            <td>Angelica Ramos</td>
                            <td>Chief Executive Officer (CEO)</td>
                            <td>London</td>
                            <td>47</td>
                            <td>2009-10-09</td>
                            <td>$1,200,000</td>
                          </tr>
                          <tr>
                            <td>Gavin Joyce</td>
                            <td>Developer</td>
                            <td>Edinburgh</td>
                            <td>42</td>
                            <td>2010-12-22</td>
                            <td>$92,575</td>
                          </tr>
                          <tr>
                            <td>Jennifer Chang</td>
                            <td>Regional Director</td>
                            <td>Singapore</td>
                            <td>28</td>
                            <td>2010-11-14</td>
                            <td>$357,650</td>
                          </tr>
                          <tr>
                            <td>Brenden Wagner</td>
                            <td>Software Engineer</td>
                            <td>San Francisco</td>
                            <td>28</td>
                            <td>2011-06-07</td>
                            <td>$206,850</td>
                          </tr>
                          <tr>
                            <td>Fiona Green</td>
                            <td>Chief Operating Officer (COO)</td>
                            <td>San Francisco</td>
                            <td>48</td>
                            <td>2010-03-11</td>
                            <td>$850,000</td>
                          </tr>
                          <tr>
                            <td>Shou Itou</td>
                            <td>Regional Marketing</td>
                            <td>Tokyo</td>
                            <td>20</td>
                            <td>2011-08-14</td>
                            <td>$163,000</td>
                          </tr>
                          <tr>
                            <td>Michelle House</td>
                            <td>Integration Specialist</td>
                            <td>Sydney</td>
                            <td>37</td>
                            <td>2011-06-02</td>
                            <td>$95,400</td>
                          </tr>
                          <tr>
                            <td>Suki Burks</td>
                            <td>Developer</td>
                            <td>London</td>
                            <td>53</td>
                            <td>2009-10-22</td>
                            <td>$114,500</td>
                          </tr>
                          <tr>
                            <td>Prescott Bartlett</td>
                            <td>Technical Author</td>
                            <td>London</td>
                            <td>27</td>
                            <td>2011-05-07</td>
                            <td>$145,000</td>
                          </tr>
                          <tr>
                            <td>Gavin Cortez</td>
                            <td>Team Leader</td>
                            <td>San Francisco</td>
                            <td>22</td>
                            <td>2008-10-26</td>
                            <td>$235,500</td>
                          </tr>
                          <tr>
                            <td>Martena Mccray</td>
                            <td>Post-Sales support</td>
                            <td>Edinburgh</td>
                            <td>46</td>
                            <td>2011-03-09</td>
                            <td>$324,050</td>
                          </tr>
                          <tr>
                            <td>Unity Butler</td>
                            <td>Marketing Designer</td>
                            <td>San Francisco</td>
                            <td>47</td>
                            <td>2009-12-09</td>
                            <td>$85,675</td>
                          </tr>
                          <tr>
                            <td>Howard Hatfield</td>
                            <td>Office Manager</td>
                            <td>San Francisco</td>
                            <td>51</td>
                            <td>2008-12-16</td>
                            <td>$164,500</td>
                          </tr>
                          <tr>
                            <td>Hope Fuentes</td>
                            <td>Secretary</td>
                            <td>San Francisco</td>
                            <td>41</td>
                            <td>2010-02-12</td>
                            <td>$109,850</td>
                          </tr>
                          <tr>
                            <td>Vivian Harrell</td>
                            <td>Financial Controller</td>
                            <td>San Francisco</td>
                            <td>62</td>
                            <td>2009-02-14</td>
                            <td>$452,500</td>
                          </tr>
                          <tr>
                            <td>Timothy Mooney</td>
                            <td>Office Manager</td>
                            <td>London</td>
                            <td>37</td>
                            <td>2008-12-11</td>
                            <td>$136,200</td>
                          </tr>
                          <tr>
                            <td>Jackson Bradshaw</td>
                            <td>Director</td>
                            <td>New York</td>
                            <td>65</td>
                            <td>2008-09-26</td>
                            <td>$645,750</td>
                          </tr>
                          <tr>
                            <td>Olivia Liang</td>
                            <td>Support Engineer</td>
                            <td>Singapore</td>
                            <td>64</td>
                            <td>2011-02-03</td>
                            <td>$234,500</td>
                          </tr>
                          <tr>
                            <td>Bruno Nash</td>
                            <td>Software Engineer</td>
                            <td>London</td>
                            <td>38</td>
                            <td>2011-05-03</td>
                            <td>$163,500</td>
                          </tr>
                          <tr>
                            <td>Sakura Yamamoto</td>
                            <td>Support Engineer</td>
                            <td>Tokyo</td>
                            <td>37</td>
                            <td>2009-08-19</td>
                            <td>$139,575</td>
                          </tr>
                          <tr>
                            <td>Thor Walton</td>
                            <td>Developer</td>
                            <td>New York</td>
                            <td>61</td>
                            <td>2013-08-11</td>
                            <td>$98,540</td>
                          </tr>
                          <tr>
                            <td>Finn Camacho</td>
                            <td>Support Engineer</td>
                            <td>San Francisco</td>
                            <td>47</td>
                            <td>2009-07-07</td>
                            <td>$87,500</td>
                          </tr>
                          <tr>
                            <td>Serge Baldwin</td>
                            <td>Data Coordinator</td>
                            <td>Singapore</td>
                            <td>64</td>
                            <td>2012-04-09</td>
                            <td>$138,575</td>
                          </tr>
                          <tr>
                            <td>Zenaida Frank</td>
                            <td>Software Engineer</td>
                            <td>New York</td>
                            <td>63</td>
                            <td>2010-01-04</td>
                            <td>$125,250</td>
                          </tr>
                          <tr>
                            <td>Zorita Serrano</td>
                            <td>Software Engineer</td>
                            <td>San Francisco</td>
                            <td>56</td>
                            <td>2012-06-01</td>
                            <td>$115,000</td>
                          </tr>
                          <tr>
                            <td>Jennifer Acosta</td>
                            <td>Junior Javascript Developer</td>
                            <td>Edinburgh</td>
                            <td>43</td>
                            <td>2013-02-01</td>
                            <td>$75,650</td>
                          </tr>
                          <tr>
                            <td>Cara Stevens</td>
                            <td>Sales Assistant</td>
                            <td>New York</td>
                            <td>46</td>
                            <td>2011-12-06</td>
                            <td>$145,600</td>
                          </tr>
                          <tr>
                            <td>Hermione Butler</td>
                            <td>Regional Director</td>
                            <td>London</td>
                            <td>47</td>
                            <td>2011-03-21</td>
                            <td>$356,250</td>
                          </tr>
                          <tr>
                            <td>Lael Greer</td>
                            <td>Systems Administrator</td>
                            <td>London</td>
                            <td>21</td>
                            <td>2009-02-27</td>
                            <td>$103,500</td>
                          </tr>
                          <tr>
                            <td>Jonas Alexander</td>
                            <td>Developer</td>
                            <td>San Francisco</td>
                            <td>30</td>
                            <td>2010-07-14</td>
                            <td>$86,500</td>
                          </tr>
                          <tr>
                            <td>Shad Decker</td>
                            <td>Regional Director</td>
                            <td>Edinburgh</td>
                            <td>51</td>
                            <td>2008-11-13</td>
                            <td>$183,000</td>
                          </tr>
                          <tr>
                            <td>Michael Bruce</td>
                            <td>Javascript Developer</td>
                            <td>Singapore</td>
                            <td>29</td>
                            <td>2011-06-27</td>
                            <td>$183,000</td>
                          </tr>
                          <tr>
                            <td>Donna Snider</td>
                            <td>Customer Support</td>
                            <td>New York</td>
                            <td>27</td>
                            <td>2011-01-25</td>
                            <td>$112,000</td>
                          </tr>
                        </tbody>
                        <tfoot>
                          <tr>
                            <th>Name</th>
                            <th>Position</th>
                            <th>Office</th>
                            <th>Age</th>
                            <th>Start date</th>
                            <th>Salary</th>
                          </tr>
                        </tfoot>
                      </table>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Data Table -->
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

export default {
  setup() {
    onMounted(() => {
      $("#miTabla").DataTable({
        paging: true, // Activar paginación
        searching: true, // Activar búsqueda
        ordering: true, // Activar ordenamiento por columnas
        pageLength: 10, // Número de filas por página
      });
    });
  },
  data() {
    return {
      formData: {
        sMuscularEsqueletico: "",
        sNerviosoCentralPeriferico: "",
        sGastrointestinal: "",
        sEndocrino: "",
        sRespiratorio: "",
        sReproductor: "",
        sSanguineo: "",
        sLinfatico: "",
        sCardiovascular: "",
        sUrinario: "",
        sOsteoarticular: "",
        sDigestivo: "",
        observaciones: "",
      },
    };
  },
  methods: {
    capturarDatos() {
      // Verificar si los campos están vacíos
      if (
        !this.formData.sMuscularEsqueletico ||
        !this.formData.sNerviosoCentralPeriferico ||
        !this.formData.sGastrointestinal ||
        !this.formData.sEndocrino ||
        !this.formData.sRespiratorio ||
        !this.formData.sReproductor ||
        !this.formData.sSanguineo ||
        !this.formData.sLinfatico ||
        !this.formData.sCardiovascular ||
        !this.formData.sUrinario ||
        !this.formData.sOsteoarticular ||
        !this.formData.sDigestivo ||
        !this.formData.observaciones
      ) {
        alert("Por favor, complete todos los campos antes de continuar.");
        return;
      }

      const datosCapturados = {
        sMuscularEsqueletico: this.formData.sMuscularEsqueletico,
        sNerviosoCentralPeriferico: this.formData.sNerviosoCentralPeriferico,
        sGastrointestinal: this.formData.sGastrointestinal,
        sEndocrino: this.formData.sEndocrino,
        sRespiratorio: this.formData.sRespiratorio,
        sReproductor: this.formData.sReproductor,
        sSanguineo: this.formData.sSanguineo,
        sLinfatico: this.formData.sLinfatico,
        sCardiovascular: this.formData.sCardiovascular,
        sUrinario: this.formData.sUrinario,
        sOsteoarticular: this.formData.sOsteoarticular,
        sDigestivo: this.formData.sDigestivo,
        observaciones: this.formData.observaciones,
      };

      console.log("Datos capturados:", datosCapturados);
    },
  },
};
</script>
