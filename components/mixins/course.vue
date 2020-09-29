<script>
import axios from 'axios'
export default {
  methods: {
    async cours() {
      const res = await axios({
        method: 'get',
        url: 'https://api.privatbank.ua/p24api/pubinfo?json&exchange&coursid=3'
      }).then((res) => res.data)
      return res
    }
  }
}
</script>
